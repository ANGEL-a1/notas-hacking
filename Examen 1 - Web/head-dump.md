# head-dump

## Descripción del Reto
Este reto de nivel introductorio (*Easy*, 50 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Explora el concepto de exposición de archivos de depuración y fugas de información crítica (*Information Disclosure*) mediante la localización de especificaciones ocultas en Swagger UI y la extracción de datos confidenciales en volcados de memoria dinámica (*Heap Dumps*).

## Análisis Técnico (Information Disclosure & Heap Dump Analysis)
Los entornos de desarrollo modernos como Node.js permiten generar archivos de diagnóstico conocidos como *Heap Dumps* o *Core Dumps*. Estos archivos clonan el estado binario completo de la memoria RAM asignada al proceso del servidor en un momento específico.

* **La Vulnerabilidad**: El fallo crítico radica en la exposición pública de un endpoint de diagnóstico (`/heapdump`). Aunque el desarrollador ocultó el acceso visual a esta ruta dentro del panel frontal de Swagger UI para evitar auditorías automáticas, la ruta permaneció registrada en el mapa estático de la especificación técnica de la API.
* **El Impacto de Seguridad**: Debido a que la memoria dinámica del backend almacena variables en texto plano, secretos de entorno, configuraciones y tokens de sesión activos durante la ejecución del proceso, cualquier atacante con acceso al volcado binario puede reconstruir y auditar la información confidencial de manera pasiva.

## Proceso de Reconstrucción
1. Se accedió a la página principal de la plataforma de noticias del reto.
2. Al inspeccionar el código fuente HTML (`Ctrl + U`), se localizó un hipervínculo hacia el panel de documentación técnica: `/api-docs`.
3. Al validar la interfaz de Swagger UI, únicamente figuraban expuestas las rutas comerciales de gestión de publicaciones (`/api/posts`).
4. Para realizar una auditoría de endpoints profunda, se descargó el script de inicialización dinámico del motor de renderizado mediante PowerShell:

   curl [http://verbal-sleep.picoctf.net:61210/api-docs/swagger-ui-init.js](http://verbal-sleep.picoctf.net:61210/api-docs/swagger-ui-init.js) -UseBasicParsing


5. Al analizar la estructura del objeto JSON `"paths"` dentro del script, se descubrió un endpoint oculto de diagnóstico omitido en el menú visual:

    ```
    "/heapdump": { "get": { "tags": ["Diagnosing"], ... } }
    ```

6. Se procedió a realizar una solicitud directa HTTP `GET` hacia la raíz del endpoint descubierto (`/heapdump`), forzando la descarga de un archivo de volcado de memoria estructurado de 11.2 MB con extensión `.heapsnapshot`.

7. Utilizando herramientas nativas de procesamiento de texto línea por línea sobre el archivo descargado, se aisló el patrón de la bandera en texto plano.

## Flag Obtenida:

picoCTF{Pat!3nt_15_Th3_K3y_dc0756a3}