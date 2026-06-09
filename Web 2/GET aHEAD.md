# GET aHEAD

## Descripción del Reto
Este reto de nivel fácil pertenece a la categoría de Explotación Web y aborda el análisis de los métodos de petición HTTP estándar. El objetivo es interactuar con una aplicación web que responde de manera distinta según el verbo HTTP utilizado, identificar la pista implícita en el nombre del desafío ("HEAD") y realizar una solicitud específica para extraer la bandera oculta en las cabeceras de la respuesta del servidor.

## Análisis de Métodos HTTP (GET vs. HEAD)
Los servidores web interpretan diferentes verbos HTTP para determinar qué acción realizar:
* **GET**: Solicita una representación del recurso especificado. Las peticiones que usan GET solo deben recuperar datos y contienen el cuerpo completo (HTML, imágenes, etc.).
* **POST**: Envía datos para que sean procesados por el recurso identificado.
* **HEAD**: Solicita una respuesta idéntica a la de una petición GET, pero **sin el cuerpo de la respuesta**. Es extremadamente útil para auditorías de red, verificar si un recurso existe o revisar los metadatos y configuraciones del servidor almacenados en las cabeceras HTTP (*Headers*).

## Proceso de Reconstrucción (Manipulación de Verbos HTTP)
Para resolver el desafío, se descartó la navegación convencional mediante el explorador web y se optó por una interacción directa con el protocolo:
* Se analizó la estructura del sitio, el cual interactuaba enviando comandos GET y POST al presionar botones interactivos.
* Se implementó un script en Python utilizando la librería `requests` para forzar explícitamente el uso del método `HEAD` contra la URL del servidor objetivo.
* Al interceptar las cabeceras de respuesta devueltas por el servidor, se localizó una cabecera personalizada no estándar (custom header) que contenía la bandera de seguridad.

## Flag Obtenida:

picoCTF{r3j3ct_th3_du4l1ty_8b13f07}