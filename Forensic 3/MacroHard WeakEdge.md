# MacroHard WeakEdge

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 60 puntos) pertenece a la categoría de Análisis Forense (*Forensics*). Explora el análisis de la estructura de archivos en formatos de documentos abiertos basados en XML (Open XML), demostrando cómo los archivos de la suite de Microsoft Office actúan como contenedores comprimidos que pueden auditarse para localizar canales encubiertos de información (*Hidden Data Disclosure*).

## Análisis Técnico (OOXML Structure & Base64 Obfuscation)
Los archivos con extensiones modernas de Microsoft Office (como `.pptm`, `.docx` o `.xlsx`) implementan la especificación internacional ECMA-376 conocida como Office Open XML (OOXML).

* **La Anatomía del Contenedor**: Independientemente de su extensión comercial, estos archivos son estructuralmente contenedores comprimidos bajo el algoritmo estándar DEFLATE (formato ZIP). Si un analista modifica la extensión del archivo a `.zip`, este puede ser descompuesto en su árbol jerárquico de directorios XML y recursos multimedia nativos.
* **El Mecanismo de Ocultación**: En este escenario, se insertó un archivo arbitrario sin extensión llamado `hidden` profundamente dentro del subdirectorio del sistema de diapositivas maestras (`ppt/slideMasters/`). Este archivo no es parseado por la interfaz gráfica de PowerPoint al abrir el documento, ocultándolo de auditorías visuales básicas y requiriendo un análisis estático forense para su detección.

## Proceso de Reconstrucción
1. Se descargó el artefacto de análisis inicial del reto: el archivo de presentación habilitado para macros `Forensics_is_fun.pptm`.
2. Utilizando la terminal local, se realizó un duplicado del archivo alterando su extensión original por una firma compatible con los descompresores nativos del sistema operativo:

   Copy-Item "Forensics_is_fun.pptm" "temp_archive.zip"


3. Se invocó la función de extracción del framework de automatización para volcar la jerarquía completa del contenedor en una carpeta independiente:


  Expand-Archive -Path "temp_archive.zip" -DestinationPath "Extracted_PPT" -Force
  

4. Se auditó el árbol de directorios resultante, aislando un archivo anómalo fuera del estándar de contenido en la ruta crítica del backend: `Extracted_PPT/ppt/slideMasters/hidden`.
5. Se leyó el contenido interno del archivo, el cual devolvió una cadena alfanumérica de texto plano ofuscada mediante el uso de espacios de separación alternos:

    ```
    Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q
    ```

6. Se unificó el string removiendo los espacios en blanco y se le aplicó un relleno criptográfico estándar de Base64 (`==`), lo que expuso la cadena reversible definitiva: `ZmxhZzoicGljb0NURntEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ==`.

7. Se ejecutó la decodificación de bytes desde la terminal local para recuperar el texto plano original en formato UTF-8, aislando con éxito la bandera de seguridad.

## Flag Obtenida:

picoCTF{D1d_u_kn0w_ppts_r_z1p5}