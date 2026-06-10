# Most Cookies

## Descripción del Reto
Este reto de nivel intermedio (150 puntos) pertenece a la categoría de Explotación Web y aborda la debilidad en la gestión de sesiones firmadas en el cliente por el framework Flask de Python. El objetivo es realizar un ataque de fuerza bruta offline sobre la firma criptográfica de la cookie de sesión para descubrir la clave secreta del servidor (*Secret Key*) y falsificar privilegios de administración.

## Análisis Técnico (Ataque Criptográfico a Cookies de Flask)
A diferencia de los esquemas de sesión en texto plano, Flask delega el almacenamiento de sesión en el cliente utilizando cookies serializadas y firmadas criptográficamente a través de un esquema basado en HMAC. Aunque el contenido del payload (en formato Base64) es legible, el backend valida su integridad comparando la firma adjunta utilizando una clave simétrica privada.

* **La Vulnerabilidad**: Si la clave secreta (`Secret Key`) del backend carece de entropía suficiente o se selecciona a partir de un diccionario de palabras predecibles, un atacante puede interceptar el token de sesión y realizar un descifrado por fuerza bruta local sin interactuar repetidamente con el servidor. Tras romper la clave, es posible firmar payloads arbitrarios válidos que el servidor procesará como legítimos (*Session Forgery*).

## Proceso de Reconstrucción
1. Se capturó el valor del token de sesión `session` transmitido por el servidor utilizando las herramientas de desarrollo.
2. Se desarrolló un script en Python utilizando los módulos nativos `itsdangerous` y `flask.json.tag` para automatizar la verificación estática de firmas criptográficas.
3. Se realizó un ataque de fuerza bruta offline iterando la cookie real contra el arreglo oficial de strings de galletas del servidor web, descubriendo la clave privada: `'black and white'`.
4. Tras obtener la clave, el script firmó criptográficamente un nuevo payload inyectando el estado de autenticación `{'very_auth': 'admin'}`.
5. Se inyectó la cookie falsificada en el navegador y se actualizó la solicitud HTTP, evadiendo el control de acceso del backend para capturar la bandera.

## Flag Obtenida:
picoCTF{cO0ki3s_yum_b8d261f0}