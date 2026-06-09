# Cookies

## Descripción del Reto
Este reto de nivel fácil (40 puntos) pertenece a la categoría de Explotación Web y aborda la manipulación de parámetros de sesión almacenados del lado del cliente. El objetivo es analizar una aplicación web que utiliza cookies HTTP para almacenar las preferencias de navegación, identificar el patrón de indexación secuencial de los datos e implementar un ataque de fuerza bruta para acceder a un perfil de sesión con privilegios elevados que aloja la bandera (flag).

## Análisis de Manipulación de Cookies (Session Hijacking)
Las cookies son pequeños fragmentos de datos que el servidor envía al navegador del usuario para mantener el estado de la navegación. Cuando un mecanismo de autorización confía únicamente en valores numéricos secuenciales fáciles de predecir (como números enteros del 0 al N) sin ninguna validación o firma criptográfica, el sistema se vuelve vulnerable:
* **Cookies HTTP**: Cabeceras de solicitud enviadas por el cliente en cada petición HTTP. En este entorno, la aplicación web valida las sesiones mediante una cookie denominada `name`.
* **Fuerza Bruta de Cookies**: Al no existir un control de integridad, un script automatizado puede alterar secuencialmente el valor del parámetro `name` de `0` a `N` para obligar al servidor a renderizar páginas correspondientes a otros índices de sesión de manera arbitraria.

## Proceso de Reconstrucción (Fuerza Bruta de Sesión)
Para resolver el desafío, se programó un script automatizado en Python que simula la interacción del navegador con el servidor web:
* Se analizó que al ingresar un nombre de galleta válido, el servidor configuraba la cookie `name` con un valor entero inicial de base.
* Se descartó la inspección manual en el navegador debido a la cantidad de iteraciones necesarias para dar con el perfil correcto de administración de manera eficiente.
* Se ejecutó el script `cookie_solucion.py` empleando el intérprete administrado para iterar secuencialmente los valores de la cookie `name` en el rango de `0` a `50`.
* Se interceptó la respuesta del servidor web cuando el valor del parámetro de sesión `name` coincidió con el identificador del perfil privilegiado (`name=18`), revelando la bandera directamente en el cuerpo del documento HTML.

## Flag Obtenida:

picoCTF{3v3ry1_l0v3s_c00k135_a4dadb49}