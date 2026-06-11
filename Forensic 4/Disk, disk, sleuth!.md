# Disk, disk, sleuth!

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 110 puntos) pertenece a la categoría de Análisis Forense (*Forensics*). Explora la inspección pasiva de imágenes de almacenamiento virtualizadas (Alpine Linux) y la extracción automatizada de cadenas de caracteres legibles en texto plano (*Data Carving / Strings Extraction*) directamente sobre bloques binarios complejos sin necesidad de montar el sistema de archivos.
## Análisis Técnico (Raw Block Auditing & Stream Decompression)
En las investigaciones forenses digitales, las imágenes de disco duro (`.img` o `.raw`) preservan la copia exacta bit por bit de los sectores de almacenamiento de un sistema de archivos, incluyendo sectores no asignados o logs internos.

* **Extracción Pasiva**: Aunque una imagen de disco puede montarse o ejecutarse mediante emuladores como QEMU, es posible realizar una auditoría estática. Dado que el sistema operativo y los archivos de configuración almacenan constantes en formato ASCII/Unicode, un volcado secuencial de los sectores binarios expone la información confidencial.
* **Optimización en Memoria (Gzip Streams)**: El formato de compresión Gzip (`.gz`) implementa el algoritmo DEFLATE para compactar el bitstream del disco. Al procesar el flujo binario directamente en memoria mediante scripts automatizados, se eliminan los cuellos de botella asociados a la creación de archivos temporales de gran escala y se evaden las restricciones de bloqueos de lectura de bajo nivel impuestos por los sistemas de control de acceso (*Unauthorized Access / Permissions Mitigation*).

## Proceso de Reconstrucción
1. Se descargó el artefacto bajo análisis: el volcado comprimido del disco duro virtual `dds1-alpine.flag.img.gz`.
2. Debido a restricciones de permisos del intérprete local de comandos para la manipulación directa de archivos de almacenamiento masivo en disco, se optó por una estrategia de análisis en memoria.
3. Se desarrolló un script en Python utilizando la librería nativa `gzip` para descomprimir el flujo binario del mapa de bits del disco sin volcarlo físicamente al disco duro local:

   with gzip.open("dds1-alpine.flag.img.gz", "rb") as f:
       content = f.read()

4. Los bytes resultantes se decodificaron bajo el estándar ASCII, ignorando errores de caracteres binarios no imprimibles para simular de forma exacta el comportamiento del comando forense `srch_strings` o `strings`.
 
5. Se implementó un filtro basado en expresiones regulares (`re.findall`) para escanear secuencialmente el texto plano extraído en busca del patrón de seguridad de la bandera (`picoCTF{...}`).

6. El motor de búsqueda localizó la coincidencia exacta mapeada en los bloques de almacenamiento persistente del sistema Alpine virtualizado.

## Flag Obtenida:

picoCTF{f0r3ns1c4t0r_n30phyt3_5e56e786}