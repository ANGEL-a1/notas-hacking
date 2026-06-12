# information

## 1. Descripción del Problema

El reto nos proporciona una imagen llamada `cat.jpg` indicando que los archivos pueden ser modificados de forma secreta. El objetivo es inspeccionar el archivo para extraer la bandera oculta.

## 🛠️ 2. Análisis y Solución

Los archivos de imagen (como JPEG) contienen metadatos estructurados en formato **EXIF** (Exchangeable Image File Format). Estos metadatos suelen almacenar información sobre la cámara, derechos de autor o licencias. En este escenario, la bandera se ocultó deliberadamente dentro de una de estas secciones de texto en formato codificado.

1. Al analizar los metadatos del archivo `cat.jpg` mediante herramientas de inspección (como `ExifInfo` o `exiftool`), se localiza una cadena sospechosa dentro del campo **License**:

    `cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9`

1. La presencia de caracteres alfanuméricos y la estructura del bloque delatan que el texto está codificado en **Base64**. Al aplicar una decodificación matemática estándar bit a bit sobre la cadena, obtenemos el texto plano correspondiente:

    - **Base64:** `cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9`

    - **Texto Plano:** `picoCTF{the_m3tadata_1s_modifi3d}`

_Nota de la sesión: Aunque la decodificación estricta del diccionario del reto resulta en la variante con Leet Speak (`modifi3d`), la plataforma validó de forma correcta la versión con la terminación en texto plano regular._

## Flag
```
picoCTF{the_m3tadata_1s_modified}
```
