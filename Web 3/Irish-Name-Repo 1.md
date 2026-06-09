# Irish-Name-Repo 1

## Descripción del Reto
Este reto de nivel medio (300 puntos) pertenece a la categoría de Explotación Web y aborda la explotación de vulnerabilidades de inyección de código SQL (SQL Injection - SQLi) en formularios de autenticación. El objetivo es analizar cómo el backend procesa las entradas del usuario al interactuar con una base de datos subyacente y diseñar un vector de ataque que altere la lógica booleana de la consulta para evadir los controles de acceso tradicionales sin poseer credenciales legítimas.

## Análisis de Inyección SQL (Autenticación Bypass)
Las inyecciones SQL ocurren cuando datos proveídos por el cliente son concatenados directamente en la construcción de una consulta SQL sin una debida sanitización o el uso de consultas preparadas (Parameterized Queries). Esto permite a un atacante inyectar sintaxis de comandos SQL:
* **Manipulación de Literales de Cadena**: El uso del carácter comilla simple (`'`) cierra prematuramente el delimitador del campo de datos en la consulta.
* **Inyección de Operadores Lógicos**: Al añadir el operador lógico `OR` junto con una condición tautológica (una expresión que siempre se evalúa como verdadera, como `'1'='1'`), se invalida el requerimiento de la evaluación de la contraseña (`AND password = ...`), forzando a la base de datos a retornar un registro de usuario válido.

## Proceso de Reconstrucción (Explotación de Formulario)
Para resolver el desafío, se interactuó de manera directa con el mecanismo de autenticación expuesto:
* Se navegó hacia la interfaz de inicio de sesión administrativo (`Admin Login`) de la aplicación web.
* Se identificó que los campos de entrada no contaban con filtros de caracteres especiales del lado del cliente ni del servidor.
* Se introdujo en el campo de nombre de usuario el payload estructurado: `admin' OR '1'='1`.
* Al procesar la solicitud, el motor de la base de datos evaluó la sentencia inyectada como verdadera para el primer registro administrativo disponible, omitiendo la validación del password secundario.
* El servidor web validó la sesión y renderizó el bloque de texto con la bandera de seguridad correspondiente.

## Flag Obtenida:

picoCTF{s0m3_SQL_85832275}