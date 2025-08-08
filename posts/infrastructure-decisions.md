# Decisiones de Infraestructura para un SaaS Minimalista

Estoy trabajando en relanzar Picstome como un servicio SaaS, y eso me ha llevado a pensar
seriamente en las plataformas y servicios que usaré para alojarlo. El objetivo es claro: lanzar
con lo mínimo necesario, sin sobreprovisionar, y escalar solo si el mercado lo pide.

## ¿Qué necesita Picstome para funcionar?

Para operar mes a mes, Picstome requiere dos servicios principales:

- **Un servidor** para manejar todas las peticiones PHP y la lógica de la aplicación.
- **Un servicio de almacenamiento** para guardar las fotos de los usuarios.

### Almacenamiento: ¿local o S3 compatible?

La forma más sencilla sería guardar las fotos en el mismo sistema de archivos del servidor.
Sin embargo, Picstome es, entre otras cosas, un servicio de almacenamiento de fotos.
Para simplificar el escalado futuro, lo ideal es usar un servicio compatible con S3.

Hoy en día, hay muchas opciones que ofrecen almacenamiento compatible con Amazon S3,
pero la mayoría de los proveedores confiables requieren un gasto mínimo mensual.
La excepción más interesante es **Cloudflare R2**: no es la opción más barata, pero su
facturación es bajo demanda, lo que permite escalar hacia arriba o abajo y pagar solo por
lo que realmente se usa. Esto ayuda a mantener la infraestructura al mínimo y evitar gastos
innecesarios al principio.

### El servidor: Hetzner como opción fuerte

Para el servidor, mi opción principal es **Hetzner**, un proveedor muy confiable y asequible.
Sus servicios cloud ofrecen recursos generosos por menos de 5 euros al mes: 4GB de RAM,
2 vCPUs y un enlace de red de 1Gbps. Para una app en fase inicial, estas especificaciones
son más que suficientes para atender a los primeros clientes.

## El mayor reto: procesamiento de imágenes

El mayor consumo de recursos en Picstome probablemente será el procesamiento de imágenes,
especialmente al generar miniaturas para galerías de fotos tomadas con cámaras de alta resolución.
Esto puede ser una tarea pesada, sobre todo en galerías con muchas fotos, y podría convertirse
en el principal cuello de botella de la app.

Sin embargo, como aún no he probado el uso real, mi plan es lanzar con el VPS más pequeño
de Hetzner, aceptar registros y clientes, y monitorear el uso de recursos. Si el servidor se
satura, escalaré a una instancia mayor. Hetzner permite escalar de forma sencilla, así que si
Picstome tiene éxito, podré atender a más clientes sin complicar la infraestructura.

## Filosofía: lanzar con lo mínimo y escalar según la demanda

La idea central de este post es lanzar un proyecto con lo mínimo indispensable, sin esperar
un éxito masivo de la noche a la mañana. Prefiero tomar decisiones de infraestructura poco a
poco, según la aceptación del mercado. Es importante mantener los pies en la tierra y crecer
sólo si es necesario, para que el servicio sea sostenible y no quemar demasiado dinero al inicio
por sobreprovisionar.

Ojalá Picstome sea un éxito y logre tener decenas de clientes satisfechos. Pero, por ahora,
mi meta es lanzar rápido, con una infraestructura mínima, y ajustar el rumbo según lo que
realmente ocurra.

---

¿Tienes experiencia lanzando SaaS con recursos mínimos? ¿Qué servicios te han funcionado
mejor? ¡Me encantaría leer tus comentarios!
