Picstome currently doesn't have any customers, but it was fun to implement a feature to delete galleries when customers stop paying for their subscriptions. Since the biggest Picstome cost is storage, we have stated in our terms and conditions that all galleries will be deleted after 7 days when the subscription expires.

So, the plan is to send reminders that a subscription is about to expire days before the actual expiration date. We thought that three reminders would be enough: 15 days, 7 days, and 1 day before expiration. Then we would send a reminder that all galleries will be deleted one day after the subscription has expired. Lastly, after 7 days of an expired subscription, we would delete all customer galleries.

To implement all this, I needed to write an artisan command to handle all this logic.

Starting by first sending expiring soon notifications, I needed a way to configure the warning days so we can later adjust the notifications timing. I created a configuration for the warning days that holds an array of days to be used to send expiring soon warnings. Next, since we use the concept of teams and personal teams, I get all the teams to check if the team subscription is still active but marked as set to end the subscription. Then, for each configured warning day, I check if we should send the reminder when the end date matches the warning target date. If so, we send the subscription expiring soon notification.

```php
// app/Console/Commands/SubscriptionsCleanupCommand.php

class SubscriptionsCleanupCommand extends Command
{
    // ...

    public function handle()
    {
        $this->notifyExpiringSoon();

        return 0;
    }

    private function notifyExpiringSoon()
    {
        $warningDays = config('picstome.subscription_warning_days', [15, 7, 1]);

        Team::has('subscriptions')->cursor()->each(function ($team) use ($warningDays) {
            $subscription = $team->subscription();

            if ($subscription && $subscription->stripe_status === 'active' && $subscription->ends_at) {
                foreach ($warningDays as $days) {
                    $targetDate = now()->addDays($days);

                    if ($subscription->ends_at->isSameDay($targetDate)) {
                        $team->owner->notify(
                            new SubscriptionExpiringSoon($days)
                        );

                        break;
                    }
                }
            }
        });
    }
}
```

The notification is pretty simple; I notify the customer that their subscription is about to expire in X days with a link to renew their subscription if they want to continue using our service.

```php
// app/Notifications/SubscriptionExpiringSoon.php

class SubscriptionExpiringSoon extends Notification
{
    // ...

    public function __construct(
        public int $daysLeft
    ) {}

    public function toMail($notifiable)
    {
        return (new MailMessage)
                    ->line(__('Your subscription expires in :days days.', ['days' => $this->daysLeft]))
                    ->action(__('Renew Subscription'), route('billing-portal'))
                    ->line(__('Thank you for using our application!'));
    }
}
```

Now, I needed to send a reminder to customers who have an expired subscription to remind them that their subscription expired and that soon we will delete all their galleries, as stated in our terms of service. This time, I created a configuration to set the number of grace period days for expired subscriptions and a config to set the days after the subscription expires that I should send the reminder. I think sending the reminder one day after the subscription expired would be the best timing to immediately remind the customer that soon their galleries will expire if the subscription is not renewed. Then, I get all the teams and check if the subscription has been marked as canceled and that the subscription ended one day ago, so I can send a subscription expired warning notification. I didn't really need to implement any logic to mark subscriptions as canceled because Laravel Cashier listens to Stripe webhooks, and in this case, it listens for the subscription canceled webhook to mark the subscription as canceled. Pretty convenient.

```php
class SubscriptionsCleanupCommand extends Command
{
    // ...

    public function handle()
    {
        $this->notifyExpiringSoon();
        $this->notifyExpired();

        return 0;
    }

    private function notifyExpired()
    {
        $expiredWarningDays = config('picstome.subscription_expired_warning_days', 1);
        $gracePeriodDays = config('picstome.subscription_grace_period_days', 7);
        $daysLeft = $gracePeriodDays - $expiredWarningDays;
        $targetDate = now()->subDays($expiredWarningDays);

        Team::has('subscriptions')->cursor()->each(function ($team) use ($targetDate, $daysLeft) {
            $subscription = $team->subscription();

            if ($subscription &&
                $subscription->stripe_status === 'canceled' &&
                $subscription->ends_at &&
                $subscription->ends_at->isSameDay($targetDate)) {
                $team->owner->notify(new SubscriptionExpiredWarning($daysLeft));
            }
        });
    }
}
```

Just like the subscription expiring soon notification, the subscription expired warning notification tells the customer that their subscription has expired and that their data will be deleted in X days if not renewed, with an action link to renew the subscription if they want to renew.

```php
// app/Notifications/SubscriptionExpiredWarning.php

class SubscriptionExpiredWarning extends Notification
{
    // ...

    public function __construct(
        public int $daysLeft
    ) {}

    public function toMail($notifiable)
    {
        return (new MailMessage)
                    ->line(__('Your subscription has expired.'))
                    ->action(__('Renew Subscription'), route('billing-portal'))
                    ->line(__('Your data will be deleted in :days days if not renewed.', ['days' => $this->daysLeft]));
    }
}
```

Lastly, if the customer subscription expired 7 days ago, I now proceed to delete their galleries. Just like before, I get all the subscriptions and check if the subscription is marked as canceled and that the grace period days have passed. If that's the case, I delete each gallery with all its photos. Behind the scenes, the `deletePhotos` method dispatches a job to delete the photo in our storage service (MEGA), so I take advantage of Laravel's queue system to defer the photo deletion load on a Laravel job.

```php
class SubscriptionsCleanupCommand extends Command
{
    // ...

    public function handle()
    {
        $this->notifyExpiringSoon();
        $this->notifyExpired();
        $this->deleteExpiredData();

        return 0;
    }

    private function deleteExpiredData()
    {
        $gracePeriodDays = config('picstome.subscription_grace_period_days', 7);

        Team::has('subscriptions')->cursor()->each(function ($team) use ($gracePeriodDays) {
            $subscription = $team->subscription();

            if ($subscription &&
                $subscription->stripe_status === 'canceled' &&
                $subscription->ends_at &&
                $subscription->ends_at->lt(now()->subDays($gracePeriodDays))) {
                $team->galleries->each(function ($gallery) {
                    $gallery->deletePhotos()->delete();
                });
            }
        });
    }
}
```

Probably I should have deferred the implementation of this data expiration for when we have actual customers in Picstome; however, it was an interesting problem to solve for the case when we start getting subscription cancellations, making it configurable and easy to adjust in the future. Hopefully, we start getting our first customers soon and that we don't really require this subscription cleanup by having a long-term relationship with our customers.
