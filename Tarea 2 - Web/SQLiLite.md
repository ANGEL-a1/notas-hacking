# SQLiLite

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 300 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Explora las vulnerabilidades de inyección de código SQL (*SQL Injection - Authentication Bypass*) sobre un motor de base de datos relacional ligero SQLite, demostrando cómo alterar la lógica de consultas de un formulario de autenticación para evadir el control de acceso sin conocer credenciales válidas.

## Análisis Técnico (SQL Injection Authentication Bypass)
Cuando un backend web recibe datos de un formulario de login de manera insegura, suele concatenar directamente las cadenas de texto del usuario dentro de la sentencia de consulta SQL. La estructura tradicional que se ejecuta internamente en el servidor se define de la siguiente manera:

$$SELECT * FROM users WHERE name='INPUT_USUARIO' AND password='INPUT_PASSWORD'$$

* **La Vulnerabilidad**: El sistema carece de mecanismos de sanitización o de consultas preparadas (*Parameterized Queries*). Al introducir caracteres de control del estándar SQL, específicamente la comilla simple (`'`), es posible cerrar de manera prematura el delimitador de la cadena de texto original en la base de datos y adjuntar directivas de lógica booleana adicionales.
* **Mecanismo de Evasión**: Mediante la inyección de la compuerta lógica `OR 1=1`, se fuerza a que la cláusula condicional completa `WHERE` se evalúe matemáticamente como **verdadera** de forma universal, sin importar el valor del usuario. Posteriormente, se anexa el operador de comentarios nativo de SQLite (`--`), lo que instruye al motor de la base de datos a ignorar por completo el resto de la sentencia original (eliminando la comprobación de la contraseña).
## Proceso de Reconstrucción
1. Se accedió al portal de autenticación segura provisto por el contenedor del reto.
2. Basado en la pista del desafío, se definió al usuario `admin` como el objetivo del bypass de identidad.
3. En el campo de texto destinado al nombre de usuario, se ingresó la carga útil (*payload*) estructurada para romper la sintaxis SQL y comentar el cierre del backend:

   admin' OR 1=1--

4. Se envió el formulario manteniendo el campo de contraseña vacío. El servidor backend procesó e inyectó la cadena, reestructurando la consulta de la siguiente forma:
   

SELECT * FROM users WHERE name='admin' OR 1=1--' AND password=''


5. Al procesarse la condición verdadera global y omitirse la validación del password, la base de datos retornó el registro administrativo y el sistema concedió el acceso.

6. Una vez en la pantalla de éxito, se inspeccionó el código fuente crudo del documento (`Ctrl + U`) debido a la indicación de que el secreto se encontraba a simple vista, localizando la bandera embebida directamente en el marcado HTML de la página.

## Flag Obtenida:

picoCTF{L00k5_l1k3_y0u_solv3d_it_9b0a4e21}