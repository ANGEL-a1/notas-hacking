# IntroToBurp

## Descripción del Reto
Este reto de nivel fácil (100 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Se centra en identificar vulnerabilidades lógicas dentro del flujo de autenticación de múltiples pasos (MFA/2FA) y explotar fallas de sanitización o validación insuficiente de parámetros de entrada (*Parameter Omission*) del lado del servidor.

## Análisis Técnico (Missing Input Validation & Authentication Bypass)
Cuando un servidor backend maneja una secuencia de formularios (como un registro de usuario seguido de una pantalla de verificación de token OTP), el código interno espera procesar un conjunto específico de variables estructuradas bajo el protocolo HTTP en el cuerpo de una solicitud `POST`.

* **La Vulnerabilidad**: El backend presenta un error crítico en el control de excepciones y en la asunción del estado de los datos. Al realizar la lógica de comparación para validar el token (por ejemplo: `if (req.body.otp !== token_real)`), el programa asume que la variable `otp` siempre será enviada por el cliente. Si un atacante altera el paquete de red y remueve por completo el parámetro `otp`, la variable se evalúa como nula (`undefined`/`null`). Debido a una mala estructuración de las condiciones lógicas, la falta del parámetro rompe la condicional de rechazo, permitiendo que el hilo de ejecución continúe con normalidad y asuma que la identidad ha sido verificada con éxito.
* **La Solución**: Interceptando el flujo HTTP mediante proxies o scripts asíncronos en la consola de desarrollo, es posible malformar deliberadamente la estructura ordinaria de la petición, enviando únicamente el usuario y contraseña para forzar el bypass en el backend.



## Proceso de Reconstrucción
1. Se accedió al portal del reto para interactuar con la página de registro.
2. Tras completar los datos primarios de usuario, el flujo redirigió a una segunda interfaz que solicitaba ingresar un código único OTP de verificación.
3. Se abrieron las Herramientas de Desarrollador del navegador (`F12`) y se ingresó a la pestaña **Console**.
4. Con el fin de evadir cualquier restricción local, se ejecutó un script asíncrono (`fetch`) para forzar un envío manual de tipo `POST` hacia el endpoint `/dashboard`, empaquetando en el cuerpo únicamente las credenciales base y omitiendo de raíz el parámetro `otp`.
5. El backend no logró validar la existencia de la propiedad del token, provocando una excepción silenciosa que evadió el muro de autenticación y retornó la respuesta administrativa exitosa con la bandera correspondiente en texto plano.

## Flag Obtenida:
picoCTF{#0TP_Bypvss_SuCc3$S_b3fa4f1a}