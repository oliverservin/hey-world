# Mi viaje resolviendo un error de red al descargar galerías en Picstome

Ser desarrollador full stack implica enfrentarse a retos técnicos que a veces parecen no tener sentido. Recientemente, tuve que solucionar un error de red que ocurría cuando los usuarios intentaban descargar galerías de fotos en [Picstome](https://picstome.com).

**¿Cómo funciona la descarga de galerías?** Cuando un usuario solicita descargar una galería, Picstome:

1. **Obtiene todas las fotos de la galería** (almacenadas en S3).
2. **Genera un archivo zip en streaming** usando la librería [maennchen/ZipStream-PHP](https://github.com/maennchen/ZipStream-PHP).
3. **Evita usar jobs en segundo plano**: En vez de crear el zip como un proceso aparte (lo que requeriría notificar al usuario por email cuando el archivo esté listo), generamos el zip al instante. Así, la experiencia es más fluida tanto para usuarios registrados como para invitados.

**¿Por qué no usar jobs?** Aunque los jobs reducen la carga del servidor, añaden fricción: el usuario debe esperar un correo y, en el caso de invitados, tendríamos que pedirles su email solo para enviarles el enlace de descarga. Hacer el zip en streaming es menos eficiente para el servidor, pero mucho más cómodo para el usuario.

**Error de red al descargar**. Algunos usuarios reportaron un “error de red” al descargar galerías grandes (cientos de fotos, varios GB). Así fue mi proceso de investigación:

**1. Sospecha inicial: Timeout de PHP**. Como el servidor actúa como proxy—descargando cada foto de S3 y generando el zip en tiempo real—lo primero que pensé fue en un timeout de PHP. Por defecto, PHP limita el tiempo de ejecución de los scripts (usualmente 30 o 60 segundos).

**Solución:**. Aumentar el tiempo de ejecución solo para la acción de descarga.

- **Archivo de configuración:**
  `php.ini`
  ```
  max_execution_time = 1200 ; 20 minutos
  ```
- **Control granular en el código:**
  En vez de cambiar el valor global, usé la función:
  ```php
  set_time_limit(1200); // 20 minutos, al inicio de la acción de descarga
  ```
  Así, solo la descarga de galerías tiene más tiempo de ejecución.

**2. El error persiste**. Después de aumentar el tiempo, el error seguía ocurriendo. Los logs de Laravel no mostraban nada relevante. Empecé a pensar que el problema podía estar en el servidor web.

**3. Revisando el servidor Caddy**. Picstome usa [Caddy](https://caddyserver.com/) como servidor web. Revisé la documentación y la configuración:

- **Archivo de configuración:**
  `Caddyfile`
- **Timeouts:**
  Por defecto, Caddy **no** tiene timeouts agresivos. No encontré problemas aquí.

**4. El verdadero culpable: Timeout de PHP-FPM**. Volví a consultar un LLM (modelo de lenguaje) para pedir ideas. Me sugirió revisar la configuración de PHP-FPM (FastCGI Process Manager), que también puede limitar el tiempo de los procesos PHP.

- **Archivo de configuración:** `www.conf` (ubicación típica: `/etc/php-fpm.d/www.conf` o `/etc/php/8.x/fpm/pool.d/www.conf`)
- **Parámetro relevante:**
  ```
  request_terminate_timeout = 1200s
  ```
  En mi servidor, este valor estaba en `60s` (1 minuto), lo que hacía que PHP matara el proceso antes de terminar la descarga.

- **Logs:** Los logs de PHP-FPM (`/var/log/php-fpm.log`) mostraban errores de timeout.

**Solución:** Actualizar `request_terminate_timeout` para que coincida con el tiempo de ejecución de PHP:

```
request_terminate_timeout = 1200s
```

No olvides reiniciar PHP-FPM después de hacer el cambio.

**5. Problema resuelto**. Tras actualizar la configuración de PHP-FPM y reiniciar el servicio, el error de red desapareció. Ahora los usuarios pueden descargar galerías grandes sin interrupciones.

## Reflexiones finales

- **Los timeouts pueden estar en varias capas**: PHP, PHP-FPM y el servidor web.
- **Revisa todos los logs**—a veces la pista está donde menos lo esperas.
- **Los LLMs pueden ayudarte** a encontrar configuraciones que pasaste por alto.

**Depurar es difícil, pero cada reto resuelto es una victoria. Si enfrentas errores de red misteriosos, revisa todas las capas—y no dudes en pedir ayuda, incluso si es a una IA.**
