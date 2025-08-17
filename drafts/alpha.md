On Picstome, we recently needed to limit contract creation access for customers. Instead of allowing unlimited contracts, free customers can now create only up to five contracts per month. To keep it simple, the monthly contract count starts on the first day of the month, regardless of when the user account was created.


## The naive approach

We could have implemented this feature naively by throwing an error message directly in the create contracts Livewire action when a free user attempts to create more than five contracts in a month.

```php
use Livewire\Volt\Component;

new class extends Component
{
    // ...

    public function save()
    {
        $contractsThisMonth = $user->contracts()
            ->whereBetween('created_at', [now()->startOfMonth(), now()->endOfMonth()])
            ->count();

        if ($contractsThisMonth >= 5 AND !$user->subscribed()) {
            $this->addError('limit.reached', 'You have reached the contract limit.');
        };

        // ...
    }
}; ?>
```

However, this would require duplicating or abstracting that logic in other areas, such as the model. We would also need to check this condition when displaying an upgrade message for a better plan or disabling the create contract form.

## Centralizing authorization with a Contract policy

A better approach I devised is to use Laravel policies. I can implement a Contract policy for the create method to check if the user is authorized to create contracts. This means verifying if the user is a free user and counting how many contracts they have created in a month. If they have already created five contracts, we deny the create contract action.

```php
class ContractPolicy {
    public function create(User $user): bool
    {
        if ($user->subscribed()) {
            return true;
        }

        $contractsThisMonth = $user->contracts()
            ->whereBetween('created_at', [now()->startOfMonth(), now()->endOfMonth()])
            ->count();

        return $contractsThisMonth < 5;
    }
}
```

## Blade integration

With this approach, we can also use the Blade directives @can or @cannot to display a message on the front end, informing the user that they cannot create new contracts and need to subscribe to continue.

```php
@cannot('create', App\Models\Contract::class)
    <flux:callout>
        <flux:callout.heading>Plan limit reached</flux:callout.heading>
        <flux:callout.text>
            Your current plan does not support creating more contracts. Upgrade your plan to create additional contracts.
        </flux:callout.text>
        <x-slot name="actions">
            <flux:button :href="route('subscribe')">Upgrade</flux:button>
        </x-slot>
    </flux:callout>
@endcannot
```

## Button & UI behavior

Additionally, with policies, we can use the cannot() and can() helpers on the user() to dynamically check if the user is authorized to create contracts. If not, we can disable the create button, preventing the user from submitting the create contract form.

```php
<flux:button
    type="submit"
    :disabled="auth()->user()->cannot('create', App\Models\Contract::class)"
>'Save'</flux:button>
```

## Livewire integration

Since our application uses Livewire, we can easily implement Livewire authorizations with $this->authorize() to validate on the backend that the user is allowed to create a new contract.

```php
use Livewire\Volt\Component;

new class extends Component
{
    // ...

    public function save()
    {
        $this->authorize('create', Contract::class);

        // ...
    }
}; ?>
```

## Conclusion & recommendation

Overall, using Laravel policies has helped us maintain clean code without duplications, leveraging existing framework features that simplify our work with maintainable code, which will pay off in the long term.

I highly recommend using Laravel policies in SaaS applications for limiting or managing quotas for features, as they help keep your application maintainable.
