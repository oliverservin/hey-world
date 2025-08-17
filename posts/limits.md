# Haciendo que los límites en un SaaS sean manejables: cuotas de contrato con Laravel Policies

En Picstome, recientemente tuvimos que limitar el acceso a la creación de contratos para los clientes. En lugar de permitir contratos ilimitados, los clientes gratuitos ahora solo pueden crear hasta cinco contratos al mes. Para simplificar, el conteo mensual de contratos comienza el primer día del mes, sin importar cuándo se creó la cuenta del usuario.

## El enfoque ingenuo

Podríamos haber implementado esta característica de manera ingenua, lanzando un mensaje de error directamente en la acción de Livewire que crea contratos, cuando un usuario gratuito intenta crear más de cinco contratos en un mes.

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

Sin embargo, esto requeriría duplicar o abstraer esa lógica en otras áreas, como en el modelo _User_. También necesitaríamos verificar esta condición al mostrar un mensaje de actualización de plan o al deshabilitar el formulario de creación de contratos.

## Centralizar la autorización con una Policy de Contract

Un mejor enfoque que ideé es utilizar las policies de Laravel. Puedo implementar una policy de Contract para el método _create_ que verifique si el usuario está autorizado a crear contratos. Esto implica comprobar si el usuario tiene una cuenta gratuita y contar cuántos contratos ha creado en un mes. Si ya ha creado cinco contratos, se denegará la acción de crear un nuevo contrato.

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

## Integración con Blade

Con este enfoque, también podemos utilizar las directivas de Blade _@can_ o _@cannot_ para mostrar un mensaje en el front-end. Este mensaje informará al usuario que no puede crear nuevos contratos y que necesita suscribirse para continuar.

```php
@cannot('create', App\Models\Contract::class)
    <flux:callout>
        <flux:callout.heading>Límite de plan alcanzado</flux:callout.heading>
        <flux:callout.text>
            Tu plan actual no permite crear más contratos. Actualiza tu plan para crear contratos adicionales.
        </flux:callout.text>
        <x-slot name="actions">
            <flux:button :href="route('subscribe')">Actualizar</flux:button>
        </x-slot>
    </flux:callout>
@endcannot
```

## UI para botón enviar

Además, con las policies, podemos usar los _helpers_ _cannot()_ y _can()_ en el usuario _user()_ para comprobar dinámicamente si el usuario está autorizado a crear contratos. Si no lo está, podemos deshabilitar el botón de crear, evitando que el usuario envíe el formulario.

```php
<flux:button
    type="submit"
    :disabled="auth()->user()->cannot('create', App\Models\Contract::class)"
>'Guardar'</flux:button>
```

## Integración con Livewire

Dado que nuestra aplicación utiliza Livewire, podemos implementar fácilmente las autorizaciones de Livewire con _$this->authorize()_ para validar en el backend que el usuario tiene permiso para crear un nuevo contrato.

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

## Conclusión y recomendación

En general, usar las policies de Laravel nos ayudó a mantener el código limpio y sin duplicaciones. Aprovechamos las funcionalidades del framework, lo que a la larga simplificará nuestro trabajo de mantenimiento del código.

Te recomiendo ampliamente utilizar las políticas de Laravel en aplicaciones SaaS para limitar o gestionar cuotas de funcionalidades, ya que facilitan el mantenimiento de la aplicación.
