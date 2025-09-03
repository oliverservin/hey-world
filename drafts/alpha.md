Picstome currently has no customers, but it was fun to implement a feature that deletes galleries when customers stop paying for their subscriptions. Since storage is the primary cost for Picstome, our terms and conditions state that all galleries will be deleted seven days after a subscription expires.

We plan to send reminders before a subscription expires. We decided that three reminders would suffice: 15 days, 7 days, and 1 day before expiration. Additionally, we will notify customers that all galleries will be deleted one day after the subscription has expired. Finally, after seven days of an expired subscription, we will delete all customer galleries.

To implement this, I wrote an artisan command to handle the logic.

Starting with the notifications for expiring subscriptions, I needed a way to configure the warning days for adjusting the notification timing later. I created a configuration for the warning days that holds an array of days to be used for sending expiring soon warnings. Since we offer both team and personal subscriptions, I retrieve all teams to check if their subscriptions are still active but marked for cancellation. For each configured warning day, I check if the end date matches the warning target date. If it does, we send the subscription expiring soon notification.

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

The notification is straightforward; it informs the customer that their subscription is about to expire in X days, along with a link to renew their subscription if they wish to continue using our service.

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

Next, I needed to remind customers with expired subscriptions that their subscription has ended and that their galleries will soon be deleted, as stated in our terms of service. I created a configuration to set the number of grace period days for expired subscriptions and another to specify when to send the reminder after expiration. I believe sending the reminder one day after expiration is the best timing to prompt the customer that their galleries will be deleted if the subscription is not renewed. I retrieve all teams and check if the subscription is marked as canceled and if it ended one day ago, allowing me to send a subscription expired warning notification. I didn't need to implement any logic to mark subscriptions as canceled because Laravel Cashier listens to Stripe webhooks, specifically for the subscription canceled webhook. This is quite convenient.

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

Similar to the subscription expiring soon notification, the subscription expired warning notification informs the customer that their subscription has expired and that their data will be deleted in X days if not renewed, with a link to renew the subscription.

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

Finally, if a customer's subscription expired seven days ago, I proceed to delete their galleries. As before, I retrieve all subscriptions and check if the subscription is marked as canceled and if the grace period days have passed. If so, I delete each gallery along with all its photos. Behind the scenes, the `deletePhotos` method dispatches a job to delete the photo in our storage service (MEGA), leveraging Laravel's queue system to defer the photo deletion load to a Laravel job.

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

I probably should have deferred the implementation of this data expiration until we have actual customers in Picstome. However, it was an interesting problem to solve in anticipation of subscription cancellations, making it configurable and easy to adjust in the future. Hopefully, we will soon acquire our first customers and maintain a long-term relationship with them, eliminating the need for this subscription cleanup.
