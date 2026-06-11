# Matryoshka doll

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 30 puntos) pertenece a la categoría de Análisis Forense (*Forensics*). Explora los conceptos de esteganografía basada en estructuras, extracción de archivos ocultos (*File Carving*) y anidación recursiva de datos confidenciales utilizando contenedores multimedia legítimos.

## Análisis Técnico (File Carving & Embedded Zip Archives)
Una técnica fundamental en forense digital es la ocultación de archivos mediante la concatenación de bytes extra al final de una imagen legítima (como un archivo JPEG o PNG).

* **La Firma del Contenedor**: Los visores de imágenes convencionales leen el archivo desde su cabecera inicial (`FF D8` para JPEG) hasta encontrar el marcador de fin de imagen (*End of Image* - `FF D9`). Cualquier byte inyectado posterior a este marcador es completamente ignorado por la interfaz gráfica, permitiendo incrustar estructuras enteras de archivos comprimidos (firmas `PK` de archivos ZIP).
* **Anidación Recursiva**: El reto emula el comportamiento de una muñeca Matryoshka tradicional, donde el descompresor debe ignorar los metadatos de renderizado de la imagen contenedora para extraer un directorio oculto (`base_images/`) que contiene la siguiente iteración, repitiendo el proceso en un bucle repetitivo hasta exponer el archivo de texto plano final.

## Proceso de Reconstrucción
1. Se descargó el artefacto de análisis forense: la imagen original `dolls.jpg`.
2. Debido a las limitaciones de utilidades automáticas lineales en entornos restringidos, se utilizó el motor nativo de descompresión de archivos planos del sistema para saltar el renderizado de la imagen y volcar la primera capa oculta:

   tar -xf dolls.jpg

3. La extracción generó el directorio `base_images/` conteniendo un segundo archivo anómalo: `2_dolls.jpg`.

4. Se ejecutó de forma recursiva el proceso de extracción sobre las capas anidadas descubiertas en la jerarquía del backend:

    - **Capa 2**: Extracción de `2_dolls.jpg` para obtener `3_dolls.jpg`.

    - **Capa 3**: Extracción de `3_dolls.jpg` para obtener `4_dolls.jpg`.

    - **Capa 4**: Extracción de la muñeca final `4_dolls.jpg`.

5. En el núcleo del último subdirectorio extraído (`base_images/`), se localizó un archivo de texto plano fuera del estándar multimedia llamado `flag.txt`.

6. Se leyó el contenido del archivo de texto, recuperando con éxito la bandera de verificación.

## Flag Obtenida:

picoCTF{LL9lb1dR4QbGe4l4iWCvGq9pdtwt7392}