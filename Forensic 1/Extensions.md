# Extensions

## Descripción del Reto
Este reto introductorio (150 puntos) pertenece a la categoría de Forense Computacional y se enfoca en el análisis de consistencia de tipos de archivos mediante el examen de metadatos y firmas digitales estructuradas (*Magic Bytes*). El desafío proporciona un archivo erróneamente indexado como `flag.txt`. El objetivo es identificar su firma estructural verdadera, corregir la extensión del contenedor y renderizar el flujo binario para extraer la bandera.

## Análisis de Firmas de Archivo (Magic Bytes)
Los sistemas operativos modernos pueden ser configurados para asociar extensiones de archivos con aplicaciones específicas, pero el análisis forense determina el tipo de datos real mediante la inspección de las cabeceras binarias en los primeros offsets del archivo.
* **Firma del Archivo Mutado**: Al realizar un volcado de strings o un análisis hexadecimal, el archivo presenta los identificadores de sección estándar del formato **Portable Network Graphics (PNG)**:
  * `IHDR`: Bloque crítico de cabecera que define los atributos geométricos de la imagen.
  * `IDAT`: Bloque contenedor del flujo de bits comprimido de los píxeles.
  * `IEND`: Delimitador que denota la terminación del flujo binario de la imagen.

## Proceso de Reconstrucción
* **Validación Forense**: Se analizó la estructura interna del archivo, confirmando la presencia de las firmas de renderizado binario nativas de un formato de imagen.
* **Corrección**: Se restauró la compatibilidad de lectura duplicando la firma hacia un contenedor adecuado utilizando comandos de PowerShell

# **Flag Obtenida**: 

`picoCTF{now_you_know_about_extensions}`
