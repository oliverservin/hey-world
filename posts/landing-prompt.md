# (Sin título)

## Dificultades de un Desarrollador con el Marketing

Ahora que trabajo en un portafolio de productos, construirlos no es mi principal dificultad, al fin y al cabo soy desarrollador web. En cambio, me resulta desafiante actuar como vendedor, intentar vender un producto y escribir textos de marketing.

## Buscando Ayuda: La Guía de Stripe

Lo primero que consideré fue buscar ayuda. Tras una búsqueda rápida, encontré un artículo en Stripe que ofrece una guía para escribir páginas landing ([Guía de Copy para Landing Page de Stripe Atlas](https://stripe.com/guides/atlas/landing-page-copy)). Después de leerlo lo econtré muy útil y práctico.

## Usando Modelos de Lenguaje para Asistir

El primer paso que tomé fue usar un modelo de lenguaje (usé GPT-4.1, pero puedes usar cualquier modelo moderno como Claude o Gemini) para crear un prompt basado en la guía que me ayudara a escribir una landing page. Este enfoque es similar a cómo uso modelos de lenguaje para ayudarme a escribir código, pero esta vez, el objetivo era crear textos efectivos para una landing page.

Le proporcioné al modelo de lenguaje la URL para que la leyera y le pedí que generara un prompt para escribir landing pages basado en el artículo.

```md
# Prompt para Copywriting de Landing Page (Basado en la Guía de Stripe Atlas)

Eres un copywriter experto en conversión. Escribe textos convincentes y altamente efectivos para una landing page. Sigue estas pautas:

1. **Enfócate en el Cliente:**
   - Dirígete al visitante directamente usando lenguaje "tú" o comienza las frases con verbos.
   - Evita el lenguaje "nosotros" o "nuestro" salvo que sea absolutamente necesario.

2. **Patrón, Textura y Brillo:**
   - Varía la longitud y estructura de las frases para lograr un tono conversacional y atractivo.
   - Sustituye palabras insípidas por sinónimos vívidos y memorables.

3. **Desactiva Objeciones:**
   - Anticipa y aborda objeciones comunes usando cláusulas "incluso si".

4. **Una Idea por Frase:**
   - Mantén las frases enfocadas y fáciles de digerir.

5. **Propósito de la Landing Page:**
   - Escribe para una audiencia y oferta específica, con un llamado a la acción (CTA) claro y relevante.
   - No escribas una página de inicio genérica.

6. **Tres Elementos Fundamentales:**
   - Da una primera impresión directa, específica y profesional.
   - Ajusta la longitud y detalle del texto según la madurez del mercado (educa si es nuevo, diferencia si es maduro).
   - Adapta el texto al nivel de conciencia del visitante (no consciente, consciente del problema, consciente de la solución, consciente del producto, muy consciente).

7. **Frameworks:**
   - Usa AIDA (Atención, Interés, Deseo, Acción) o PAS (Problema, Agitación, Solución) para estructurar el texto.
   - Aplica la Regla de Uno: un lector, una gran idea, una promesa, una oferta.

8. **Sé Específico y Visual:**
   - Usa lenguaje y datos concretos y específicos.
   - Visualiza números o logros para hacerlos comprensibles.

9. **Aclara Para Quién Es:**
   - Incluye una declaración "ideal para" cerca del inicio para ayudar a los visitantes a identificarse.

10. **Itera y Prueba:**
    - Escribe textos fáciles de probar y refinar.

**Input:**
- Nombre del producto/servicio
- Qué hace
- Audiencia objetivo
- Beneficio(s) principal(es)
- Objeciones o dudas que puedan tener los clientes
- Madurez del mercado (nuevo/emergente o establecido/maduro)
- Nivel de conciencia del cliente
- Pruebas, datos o testimonios

**Output:**
- Titular
- Subtitular
- Texto principal (incluyendo características, beneficios y (opcional) prueba social)
- CTA claro y específico
- Declaración "ideal para"
- Frases para manejar objeciones
- Pruebas visuales o basadas en datos (opcional)

Escribe en un estilo claro, persuasivo y centrado en el cliente. Haz el texto específico, memorable y accionable.
```

## Inputs Requeridos para el Prompt

Sin embargo, usar este prompt requiere que proporcione ocho cosas, ya que está basado en la guía de Stripe:

```md
- Nombre del producto/servicio
- Qué hace
- Audiencia objetivo
- Beneficio(s) principal(es)
- Objeciones o dudas que puedan tener los clientes
- Madurez del mercado (nuevo/emergente o establecido/maduro)
- Nivel de conciencia del cliente
- Pruebas, datos o testimonios (opcional—omitir si aún no tienes)
```

Aparte del nombre del producto y su función, al principio no tenía nada más. Creo que esto es normal en emprendedores técnicos como yo, que se enfocan más en construir.

## Escribiendo el Borrador Inicial

Así que escribí un borrador que describe el propósito del producto, el problema que resuelve y cómo funciona. No tenía testimonios aún, así que me enfoqué en dejar claro y accionable el valor del producto.

```md
Terrific Poll es un servicio que te permite crear encuestas fácilmente para incrustar en newsletters usando cualquier servicio de email.

Incluso si tu servicio de newsletter no soporta encuestas, puede requerir una mejora de plan o un complemento de pago.

Primero, creas una encuesta asignándole un nombre interno, escribiendo la pregunta y agregando hasta 10 opciones de respuesta.

Luego puedes copiar la encuesta para incrustarla fácilmente en servicios como Beehiiv, Brevo, EmailOctopus, Ghost, HubSpot, Kit, Loops, MailerLite y Sendy.

La encuesta copiada incluye tu pregunta y enlaces a las opciones de respuesta. Cuando el destinatario hace clic en una opción, se abre una página para confirmar su selección. El email de contacto se rellena automáticamente usando las etiquetas de tu servicio de newsletter y se envía la respuesta.

Cuando empiezas a recibir respuestas, el panel de control de tu encuesta mostrará el número de respuestas recibidas y un indicador de porcentaje para cada opción. También puedes acceder a una tabla detallada con las respuestas por opción, la fecha y el email de contacto (si se proporciona) de quien respondió.
```

## Rellenando los Huecos con Modelos de Lenguaje

Ahora que he escrito mi borrador, puedo utilizar modelos de lenguaje nuevamente para ayudarme a abordar las partes faltantes requeridas por el prompt para redactar el texto de la landing page. Después de generar el borrador, lo revisé para asegurar su claridad y veracidad. Editar lo que nos proporciona la IA es crucial.

### Qué Hace el Producto

La primera tarea fue pedirle al modelo de lenguaje que identificara, en sus propias palabras, qué hace el producto.

Lo hizo muy bien resumiendo lo que hace mi producto con mínima corrección.

```md
Terrific Poll es un servicio que permite a los usuarios crear e incrustar encuestas fácilmente en emails de newsletters, sin importar el servicio de newsletter que usen.

- Crear encuestas: Los usuarios pueden crear una encuesta dándole un nombre interno, escribiendo una pregunta y agregando hasta 10 opciones de respuesta.
- Incrustar en newsletters: El servicio genera contenido de encuesta que puede incrustarse en plataformas populares de newsletters (por ejemplo, Beehiiv, Brevo, EmailOctopus, Ghost, HubSpot, Kit, Loops, MailerLite, Sendy), incluso si esas plataformas no soportan encuestas nativamente.
- Recopilación fácil de respuestas: Cada opción de la encuesta es un enlace. Cuando el destinatario hace clic en una respuesta, se le lleva a una página de confirmación donde su selección se rellena automáticamente (usando las etiquetas de merge del servicio de newsletter) y se envía.
- Panel y analíticas: Tras recopilar respuestas, los usuarios pueden ver un panel que muestra:
    - El número de respuestas por opción
    - Indicadores de porcentaje por respuesta
    - Una tabla detallada con cada respuesta, la fecha y el email de contacto (si se proporciona)

Terrific Poll te permite crear, incrustar y rastrear encuestas en cualquier newsletter, con recopilación fácil de respuestas y analíticas, incluso si tu servicio de newsletter no soporta encuestas nativamente.
```

### Identificando la Audiencia Objetivo

Luego, le pedí que pensara en la audiencia objetivo. Identificó eficazmente como principal audiencia a los creadores y editores de newsletters.

```md
1. Creadores y Editores de Newsletters
   - Escritores independientes, bloggers y creadores de contenido que envían newsletters regularmente y quieren involucrar a su audiencia con encuestas.
   - Pequeñas empresas y startups que usan newsletters para marketing, feedback o engagement.

1. Equipos de Marketing
   - Marketers de email que buscan añadir elementos interactivos (como encuestas) a sus campañas sin pagar planes caros o complementos.
   - Agencias que gestionan newsletters para varios clientes en diferentes plataformas.

2. Organizaciones que Usan Diversas Plataformas de Email
   - Empresas o grupos que usan plataformas que no soportan encuestas nativamente (ej. Beehiiv, Brevo, EmailOctopus, Ghost, HubSpot, Kit, Loops, MailerLite, Sendy).
   - ONGs, clubes o instituciones educativas que quieren recopilar opiniones de sus listas de correo.

3. Quienquiera que Quiera Encuestas en Email Sin Complicaciones Técnicas
   - Usuarios que quieren una solución sin código, de copiar y pegar, para añadir encuestas a emails.
   - Personas que quieren analíticas (conteo de respuestas, porcentajes, emails de los respondientes) sin construir su propio sistema.

Terrific Poll es ideal para cualquiera que envíe newsletters y quiera añadir encuestas fácilmente—especialmente si su plataforma no soporta encuestas nativamente o requiere una mejora de pago para hacerlo.
```

### Resumiendo los Beneficios Principales

El siguiente paso fue describir los principales beneficios de mi producto. El modelo los resumió de manera efectiva, destacando ocho ventajas clave.

```
1. Compatibilidad Universal
   - Funciona con cualquier servicio de newsletters, incluso los que no soportan encuestas nativamente.
   - No necesitas cambiar de plataforma ni pagar complementos caros.

2. Creación Fácil de Encuestas
   - Interfaz simple para crear encuestas: solo nombra tu encuesta, escribe la pregunta y agrega hasta 10 opciones.
   - No se requieren habilidades técnicas ni de programación.

3. Incrustación Sin Fricciones
   - Genera contenido de encuesta que puedes copiar y pegar en cualquier plataforma de newsletters.
   - Soporta servicios populares como Beehiiv, Brevo, EmailOctopus, Ghost, HubSpot, Kit, Loops, MailerLite y Sendy.

4. Recopilación de Respuestas Sin Obstáculos
   - Los destinatarios hacen clic en un enlace en el email para votar—sin formularios ni pasos extra.
   - El email de contacto se rellena automáticamente usando etiquetas de merge, facilitando la respuesta.

5. Analíticas y Panel en Tiempo Real
   - Ve instantáneamente cuántas respuestas recibió cada opción.
   - Consulta el desglose porcentual de cada respuesta.
   - Accede a una tabla detallada con datos de respuesta, incluyendo fecha y (si está disponible) email de contacto.

6. Sin Bloqueo de Plataforma
   - No estás atado a un proveedor de email ni obligado a mejorar tu plan solo para usar encuestas.

8. Mayor Engagement
   - Las encuestas aumentan la interactividad y el engagement en newsletters, ayudándote a entender mejor a tu audiencia.

Terrific Poll facilita añadir encuestas interactivas a cualquier newsletter, recopilar respuestas con un solo clic y ver analíticas detalladas—todo sin complicaciones técnicas ni limitaciones de plataforma.
```

### Abordando Objeciones

Luego, me enfoqué en frases para abordar objeciones, que son dudas legítimas que los clientes potenciales pueden tener. El modelo generó diez temas principales de objeciones.

```md
1. Entregabilidad y Spam
   - "¿Agregar enlaces de encuesta afectará la entregabilidad de mis emails o aumentará la probabilidad de que sean marcados como spam?"

2. Privacidad y Seguridad de Datos
   - "¿Cómo se maneja y protege la información de mi audiencia (especialmente los emails)?"
   - "¿Terrific Poll cumple con GDPR?"

3. Personalización y Branding
   - "¿Puedo personalizar el aspecto de la encuesta y la página de confirmación para que coincida con mi marca?"
   - "¿Mis suscriptores verán el branding de Terrific Poll en vez del mío?"

4. Experiencia de Usuario
   - "¿Mis suscriptores se confundirán al hacer clic y ser llevados a una página de confirmación?"
   - "¿El proceso es fluido o añade fricción?"

5. Limitaciones de Integración
   - "¿Funciona con mi plataforma de newsletters y etiquetas de merge?"
   - "¿Qué pasa si mi plataforma no soporta etiquetas de merge o tiene soporte limitado?"

6. Precisión en el Rastreo de Respuestas
   - "¿Qué tan preciso es el rastreo de respuestas, especialmente si la gente reenvía emails o hace clic varias veces?"
   - "¿Se puede votar más de una vez?"

7. Costo y Valor
   - "¿Vale la pena pagar por este servicio si algunas plataformas ofrecen encuestas básicas gratis o como complemento de pago?"
   - "¿Hay costos ocultos o limitaciones?"

8. Soporte Técnico y Fiabilidad
   - "¿Qué pasa si algo sale mal—qué tan rápido puedo obtener soporte?"
   - "¿El servicio es confiable y siempre está disponible?"

9. Propiedad y Exportación de Datos
   - "¿Puedo exportar fácilmente los resultados y datos de mi encuesta?"
   - "¿Conservo la propiedad de mis datos?"

10. Accesibilidad
    - "¿Los enlaces de encuesta y páginas de confirmación son accesibles para todos, incluyendo quienes usan tecnologías de asistencia?"
```

Podría haber respondido cada una de las preguntas. Sin embargo, dado que estamos utilizando la IA, también le pedí al modelo que generara posibles respuestas a cada objeción.

```md
1. Entregabilidad y Spam
   - "¿Agregar enlaces de encuesta afectará la entregabilidad de mis emails o aumentará la probabilidad de que sean marcados como spam?"

**Respuesta:** Terrific Poll usa formatos de enlace estándar y reputados, compatibles con todos los proveedores de email principales. Nuestros enlaces están diseñados para evitar disparadores comunes de spam y nunca incluyen adjuntos ni redirecciones sospechosas. Como con cualquier email, seguir buenas prácticas—como usar un dominio verificado y evitar enlaces excesivos—ayuda a mantener alta la entregabilidad.

2. Privacidad y Seguridad de Datos
   - "¿Cómo se maneja y protege la información de mi audiencia (especialmente los emails)?"
   - "¿Terrific Poll cumple con GDPR?"

**Respuesta:** Nos tomamos la privacidad y seguridad de los datos muy en serio. Todos los datos, incluidos los emails, se encriptan en tránsito y en reposo. Nunca vendemos ni compartimos la información de tu audiencia con terceros. Terrific Poll está diseñado pensando en GDPR y otras regulaciones de privacidad, y ofrecemos herramientas para que gestiones, exportes o elimines datos según lo necesites.

3. Personalización y Branding
   - "¿Puedo personalizar el aspecto de la encuesta y la página de confirmación para que coincida con mi marca?"
   - "¿Mis suscriptores verán el branding de Terrific Poll en vez del mío?"

**Respuesta:** Por ahora, la página de confirmación no puede personalizarse con los colores, logo o mensajes de tu marca. Sin embargo, Terrific Poll no muestra branding visible a tus suscriptores—la única referencia es el dominio en la barra de direcciones del navegador. La experiencia se mantiene limpia y neutral, para que la atención de tu audiencia esté en la pregunta y opciones de tu encuesta.

4. Experiencia de Usuario
   - "¿Mis suscriptores se confundirán al hacer clic y ser llevados a una página de confirmación?"
   - "¿El proceso es fluido o añade fricción?"

**Respuesta:** El proceso está diseñado para ser lo más simple posible: un clic lleva al suscriptor a una página de confirmación clara donde su elección se rellena automáticamente. Este paso extra ayuda a validar votos y da a los usuarios la oportunidad de confirmar su selección, mejorando la calidad de los datos sin añadir confusión.

5. Limitaciones de Integración
   - "¿Funciona con mi plataforma de newsletters y etiquetas de merge?"
   - "¿Qué pasa si mi plataforma no soporta etiquetas de merge o tiene soporte limitado?"

**Respuesta:** Terrific Poll es compatible con las principales plataformas de newsletters y soporta una amplia variedad de etiquetas de merge para rellenar información del suscriptor. Si tu plataforma tiene soporte limitado, la encuesta igual funcionará—los destinatarios pueden ingresar su email manualmente si es necesario. Ofrecemos guías detalladas para las plataformas más populares y podemos ayudarte con configuraciones personalizadas.

6. Precisión en el Rastreo de Respuestas
   - "¿Qué tan preciso es el rastreo de respuestas, especialmente si la gente reenvía emails o hace clic varias veces?"
   - "¿Se puede votar más de una vez?"

**Respuesta:** Cada respuesta se rastrea individualmente y usamos emails (cuando están disponibles) para ayudar a prevenir votos duplicados. Aunque reenviar emails puede permitir respuestas múltiples desde el mismo enlace, nuestro panel destaca posibles duplicados para que los revises. Para la mayoría de los casos, esto ofrece una imagen confiable y precisa de las preferencias de tu audiencia.

7. Costo y Valor
   - "¿Vale la pena pagar por este servicio si algunas plataformas ofrecen encuestas básicas gratis o como complemento de pago?"
   - "¿Hay costos ocultos o limitaciones?"

**Respuesta:** Terrific Poll ofrece compatibilidad universal, analíticas avanzadas y personalización que la mayoría de las funciones integradas o complementos no pueden igualar. No hay tarifas ocultas—nuestros precios son transparentes y tienes acceso completo a todas las funciones. Para muchos usuarios, el tiempo ahorrado y el mayor engagement justifican la inversión.

8. Soporte Técnico y Fiabilidad
   - "¿Qué pasa si algo sale mal—qué tan rápido puedo obtener soporte?"
   - "¿El servicio es confiable y siempre está disponible?"

**Respuesta:** Ofrecemos soporte al cliente rápido por email y chat, con la mayoría de los problemas resueltos en un día hábil. Nuestra infraestructura está diseñada para la fiabilidad, con alta disponibilidad y monitoreo regular para asegurar que tus encuestas siempre estén disponibles.

9. Propiedad y Exportación de Datos
   - "¿Puedo exportar fácilmente los resultados y datos de mi encuesta?"
   - "¿Conservo la propiedad de mis datos?"

**Respuesta:** Por supuesto. Puedes exportar los resultados de tu encuesta en cualquier momento en formato CSV. Siempre conservas la propiedad total de tus datos y nunca los usamos para ningún propósito que no sea proveer el servicio.

10. Accesibilidad
    - "¿Los enlaces de encuesta y páginas de confirmación son accesibles para todos, incluyendo quienes usan tecnologías de asistencia?"

**Respuesta:** La accesibilidad es una prioridad para nosotros. Nuestros enlaces y páginas de confirmación están diseñados para cumplir con los estándares modernos de accesibilidad (como WCAG), asegurando que todos los usuarios—including quienes usan lectores de pantalla o tecnologías de asistencia—puedan participar sin barreras.
```

### Evaluando la Madurez del Mercado

La tarea consistió en determinar la madurez del mercado, es decir, si el mercado del producto es nuevo o emergente. Personalmente, no sabía cómo evaluarlo; probablemente es algo que haría un buen especialista en marketing. La madurez del mercado influye en la cantidad de educación que necesitas proporcionar a tu audiencia. Si tu producto pertenece a una categoría nueva, será necesario explicar más. Si se trata de un mercado establecido, será importante destacar las diferencias.

Pedirle al modelo de lenguaje que determine la madurez del mercado fue una solución rápida para mi falta de conocimiento por ahora.

```md
El mercado general de email marketing es maduro, pero el nicho específico de encuestas universales, incrustables y sin código para newsletters es nuevo y emergente. Hay demanda clara, pero el espacio aún no está saturado.

**Nivel de Conciencia del Cliente: De Consciente del Problema a Consciente de la Solución**

- Consciente del Problema:
    La mayoría de los clientes potenciales (creadores de newsletters, marketers, etc.) saben que:
    - Quieren involucrar más a su audiencia.
    - Su plataforma actual de newsletters no soporta encuestas, o solo lo hace con limitaciones o costo extra.
    - Quizá han probado alternativas (como Google Forms) pero las encontraron poco integradas o incómodas.
- Consciente de la Solución:
    Algunos clientes saben que existen herramientas de "encuestas por email", pero:
    - No saben que hay una solución universal, fácil y sin código disponible.
    - No conocen Terrific Poll específicamente.
    - No se imaginan lo fluida y agnóstica de plataforma que puede ser una solución.
- Aún No Consciente del Producto:
    La mayoría de la audiencia objetivo probablemente no conoce Terrific Poll por nombre ni sus beneficios únicos, salvo que hayan buscado específicamente este tipo de herramienta.

La audiencia de Terrific Poll es mayormente consciente del problema y de la solución—saben que quieren añadir encuestas a emails y conocen algunas soluciones, pero aún no están familiarizados con Terrific Poll como la mejor o más fácil opción.
```

## Generando el Copy Final de la Landing Page

Ese fue el último punto. Ahora pude usar mi prompt para pedirle al modelo de lenguaje que generara el copy de mi landing page con todos los inputs de mi producto.

Aquí está el copy final de la landing page que obtuve (tras algunos retoques manuales). Nota: Como aún no tenía testimonios ni prueba social, me enfoqué en los beneficios del producto y un llamado a la acción claro.

---

# Terrific Poll: Añade Encuestas Interactivas a Cualquier Newsletter

**Crea e incrusta encuestas fácilmente en tus newsletters—sin código, sin bloqueo de plataforma.**

Terrific Poll te permite involucrar a tu audiencia con encuestas interactivas, incluso si tu servicio de newsletters no soporta encuestas nativamente. Solo crea tu encuesta, copia y pega el contenido, y comienza a recopilar respuestas al instante.

- Funciona con Beehiiv, Brevo, EmailOctopus, Ghost, HubSpot, Kit, Loops, MailerLite, Sendy y más
- No necesitas mejorar tu plan ni pagar complementos
- Recopilación de respuestas con un clic y emails de contacto pre-rellenados
- Analíticas en tiempo real y resultados exportables

**Ideal para:**
- Creadores de newsletters, marketers, agencias y organizaciones que usan cualquier plataforma de email

**Manejo de objeciones:**
- "¿Esto afecta la entregabilidad?" No—nuestros enlaces están diseñados para evitar disparadores de spam.
- "¿Mis datos están seguros?" Sí—tus datos se encriptan y nunca se comparten.
- "¿Puedo personalizar el aspecto?" La experiencia es limpia y neutral, sin branding visible de Terrific Poll.

**¿Listo para aumentar el engagement?**
[Comienza tu primera encuesta ahora]

---

Si aún no tienes testimonios ni prueba social, está perfectamente bien. Enfócate en dejar claro el valor de tu producto e invita a los visitantes a probarlo o unirse a tu lista de acceso temprano. A medida que recibas feedback de usuarios, puedes actualizar tu landing page con citas o datos que muestren el impacto de tu producto.

Hice algunos cambios manuales para ajustarlo a mi gusto, pero en general, los cambios fueron mínimos.

## Reflexiones sobre el Proceso

El modelo de lenguaje realmente me ayudó a entender mejor el mercado al que entra mi producto y las posibles audiencias objetivo. El prompt fue efectivo para generar un borrador de landing page que luego usé para diseñar la página de mi producto.

Es asombroso que los modelos de lenguaje puedan ayudarnos con este trabajo. Habría necesitado invertir mucho tiempo en investigación de mercado o contratar a un copywriter profesional.

Usar modelos de lenguaje como herramienta, igual que hago para escribir código, en áreas fuera de mi experiencia realmente me ha ayudado a cubrir mis vacíos de conocimiento en esos temas, y podría ayudarte a ti también.
