On Picstome, we recently needed to limit contract creation access for customers. Instead of allowing unlimited contracts, free customers can now create only up to five contracts per month.

We could have implemented this feature naively by throwing an error message directly in the create contracts Livewire action when a free user attempts to create more than five contracts in a month.

However, this would require duplicating or abstracting that logic in other areas, such as the model. We would also need to check this condition when displaying an upgrade message for a better plan or disabling the create contract form.

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

Additionally, with policies, we can use the cannot() and can() helpers on the user() to dynamically check if the user is authorized to create contracts. If not, we can disable the create button, preventing the user from submitting the create contract form.

```php
<flux:button
    type="submit"
    :disabled="auth()->user()->cannot('create', App\Models\Contract::class)"
>'Save'</flux:button>
```

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

Overall, using Laravel policies has helped us maintain clean code without duplications, leveraging existing framework features that simplify our work with maintainable code, which will pay off in the long term.

I highly recommend using Laravel policies in SaaS applications for limiting or managing quotas for features, as they help keep your application maintainable.

## Remaining gaps and recommended fixes

Before shipping this approach we identified several logical gaps and recommended fixes:

- Clarify timezone choice and boundary handling: decide whether counts use user timezone or UTC and document how month boundaries are handled to avoid off-by-one errors.
- State treatment of soft-deleted or draft contracts: explicitly exclude or include soft-deleted/draft contracts in counts and ensure queries use whereNull('deleted_at') or appropriate scopes.
- Delegate counting to a UsageService/repository: move counting logic out of the policy into a UsageService with a signature like: public function contractsCreatedThisPeriod(User $user, Carbon $start, Carbon $end): int; this makes it easier to cache, test, and reuse.
- Race conditions and atomic enforcement: warn that policy checks alone are vulnerable to races; enforce limits server-side with atomic counters, database transactions, or by performing a final atomic check at write time.
- Performance and caching: for large datasets consider precomputed counters or cached usage values and ensure proper DB indexes on created_at and user_id for efficient counting.
- UX additions: show remaining quota and the reset date in the UI so users understand limits and when they will be able to create more.
- Testing and monitoring: add unit tests for the policy and UsageService and Livewire integration tests; add monitoring/alerts for quota enforcement failures or spikes in denied requests.
- Error handling: throw AuthorizationException with a helpful message when denying actions so Livewire and APIs can present actionable feedback to users.

Addressing these gaps will make the quota enforcement robust, performant, and user-friendly.

