# Timer

## Descripción del Reto
Este reto de nivel intermedio (100 puntos)  El objetivo consiste en analizar un archivo empaquetado de aplicación Android (.APK) para extraer información sensible o secretos comerciales (llaves/banderas) que los desarrolladores suelen dejar expuestos por error dentro del sistema de archivos interno de la app.

## Análisis Técnico (Android Package Disassembly & Resource Inspection)
Un archivo con extensión `.apk` funciona a nivel lógico como un contenedor comprimido estándar basado en el formato ZIP. Dentro de su estructura, almacena el manifiesto de la app, el código de las actividades ejecutable de Dalvik (`classes.dex`), y múltiples subcarpetas de recursos gráficos y de texto (`res/`).

* **La Vulnerabilidad**: Los entornos de desarrollo móvil suelen centralizar cadenas de texto estáticas en archivos de configuración planos (como `strings.xml`). Al compilar el paquete de producción, si el código fuente no se somete a procesos de ofuscación estrictos (ej. ProGuard/R8) o si los secretos se queman directamente en los assets del contenedor, cualquier analista puede extraer los strings legibles sin necesidad de emular la app dinámicamente.
* **La Solución**: En lugar de configurar entornos de descompilación pesados (como JADX-GUI o MobSF), es posible interactuar de forma nativa con el paquete utilizando las librerías estándar de Python `zipfile` y `re`. Al tratar el APK como un flujo binario ZIP en memoria, se puede extraer el código comprimido y aplicar expresiones regulares para filtrar y mapear cualquier coincidencia de texto que exponga el formato del secreto buscado.

## Proceso de Reconstrucción
1. Se descargó el instalador de la aplicación móvil `timer (1).apk`.
2. Se desarrolló un script de automatización en Python (`apk_flag_finder.py`) diseñado para abrir el contenedor de manera transparente y realizar un escaneo recursivo de descriptores de archivos internos.
3. El script aplicó la expresión regular `picoCTF\{.*?\}` sobre el contenido crudo decodificado de los recursos de la app, evitando la necesidad de extraer manualmente los subdirectorios.
4. El motor de búsqueda localizó la coincidencia exacta dentro de las cadenas de texto empaquetadas, revelando la bandera en texto plano:

# Flag 

   picoCTF{t1m3r_r3v3rs3d_succ355fully_17496}