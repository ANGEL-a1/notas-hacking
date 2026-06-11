# Local Authority

## Descripción del Reto
Este reto de nivel básico (100 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Explora las vulnerabilidades asociadas a la autenticación del lado del cliente (*Client-Side Authentication*), donde las reglas de negocio y los datos de validación de identidad se delegan por completo al navegador del usuario en lugar de procesarse de manera segura en el backend.

## Análisis Técnico (Exposed Client-Side Credentials)
En arquitecturas web seguras, cualquier proceso de verificación de credenciales debe ocurrir de forma aislada en el backend (*Server-Side*), resguardado por una base de datos o lógica inaccesible para el público. Cuando un desarrollador delega esta responsabilidad a un archivo JavaScript transferido de forma local al cliente, expone de forma íntegra las directivas lógicas de la aplicación.

* **La Vulnerabilidad**: El portal web hace uso de un archivo estático de JavaScript para ejecutar la función de inicio de sesión. Al estar almacenadas las credenciales válidas en texto plano dentro de una condicional estricta (`===`), cualquier auditor web con acceso a las herramientas de desarrollo del navegador puede descargar e inspeccionar la lógica cruda, obteniendo el usuario y la contraseña sin requerir una fase de fuerza bruta.
* **La Solución**: Cambiar el contexto de inspección de las herramientas de desarrollo hacia la pestaña de recursos locales (`Page`) para examinar de manera directa los scripts complementarios del portal.

## Proceso de Reconstrucción
1. Se accedió al formulario de inicio de sesión principal provisto por la instancia del reto.
2. Al intentar un inicio de sesión con credenciales arbitrarias falsas, el portal devolvió un mensaje estático de error administrado por la página `login.php`.
3. Se invocaron las Herramientas de Desarrollador (`F12`), navegando de forma específica hacia la pestaña **Sources** y conmutando el subpanel al árbol de archivos del sitio (**Page**).
4. Se identificó la existencia del script complementario **`secure.js`**, el cual contenía la rutina de validación de texto plano en el navegador:

   function checkPassword(username, password) {
   if( username === 'admin' && password === 'strongPassword098765' ) {
   return true;
   } else {
   return false;
   }
   }

5. Se extrajeron las credenciales del código fuente (`admin` / `strongPassword098765`), se reingresaron en el formulario principal y se presionó el botón de acceso. El sistema local validó la condición de éxito y el backend expuso la bandera final.


## Flag Obtenida:

picoCTF{j5_15_7r4n5p4r3n7_b0c2c9cb}