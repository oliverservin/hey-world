# Starter Kit de Laravel para SaaS

Hoy estoy lanzando mi propio starter kit con una estructura y decisiones muy definidas para Laravel, que se ha convertido en mi punto de partida para la mayoría de mis proyectos SaaS.

Después de trabajar en varios proyectos SaaS, noté que siempre terminaba armando la misma base: autenticación, suscripciones, manejo de errores y una buena interfaz de usuario. Así que decidí empaquetar todo eso en un solo kit, y ahora está disponible.

Este proyecto parte del excelente [Laravel Livewire Starter Kit](https://github.com/laravel/laravel-livewire-starter-kit), pero le he añadido mejoras y herramientas que uso en mis propios productos.

Incluye Laravel Cashier para Stripe y Stripe Checkout, con un solo plan de suscripción y 30 días de prueba gratis. Además, incorpora el middleware `EnsureUserIsSubscribed`, que asegura que el usuario tenga una suscripción activa incluso para acceder al dashboard, lo que motiva a los usuarios a suscribirse y aprovechar el trial para seguir usando la app.

Uso el paquete Flux Pro (licencia de pago) para agregar componentes de UI listos para la mayoría de las necesidades SaaS. Es una base genial para crear interfaces atractivas y funcionales rápidamente.

También integré Honeybadger para el tracking de errores; el plan gratuito es muy generoso, ideal para proyectos en fase inicial.

El starter kit está disponible en [GitHub](https://github.com/terrific-mx/starter-kit) bajo licencia MIT. Planeo mantenerlo actualizado según crezcan mis pequeños negocios SaaS (si es que sucede).

Si buscas una base sólida, con criterios claros y lista para lanzar tu próximo SaaS con Laravel, dale un vistazo y cuéntame qué te parece. Espero que te sea útil y te ayude a lanzar tus ideas más rápido.

[Repositorio en GitHub](https://github.com/terrific-mx/starter-kit)
