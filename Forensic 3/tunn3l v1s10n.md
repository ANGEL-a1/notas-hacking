# tunn3l v1s10n

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 40 puntos) pertenece a la categoría de Análisis Forense (*Forensics*). Explora la reconstrucción estática de estructuras binarias mediante la reparación de cabeceras de mapas de bits (*BMP Headers*), cálculo de alineación de estructuras por padding de bytes y evasión de contramedidas de desorientación (*Anti-Analysis Bypass / Fake Flags*).

## Análisis Técnico (Row Padding Alignment & Countermeasures)
El formato BMP requiere que cada fila de píxeles esté estrictamente alineada a un múltiplo de 4 bytes (Row Padding). Si las dimensiones declaradas en la cabecera no coinciden exactamente con la tasa de compresión y padding físico de la matriz de pixeles, el renderizado se desfasa.

* **La Contramedida (Fake Flag Troll)**: El creador del reto introdujo una bandera falsa (`picoCTF{qu35710n_m4rk_c3nt3r_13_by735}`) visible únicamente cuando el lienzo se expande de forma desproporcionada. Esto funciona como un señuelo para evadir herramientas automatizadas o análisis superficiales.
* **El Cálculo Forense Exacto**:
  * Tamaño total del archivo: 2,893,454 bytes.
  * Tamaño de cabeceras: 54 bytes.
  * Buffer de píxeles puro: 2,893,400 bytes.
  * Ancho original: 1134 píxeles (3402 bytes netos). Añadiendo los 2 bytes de alineación requeridos por la especificación BMP, cada fila física mide exactamente 3404 bytes.
  * Alto Real Matemático: $2,893,400 \div 3404 = \mathbf{850 \text{ píxeles}}$.

## Proceso de Reconstrucción
1. Se identificó el archivo como un Bitmap dañado debido a sus bytes iniciales `42 4D` (`BM`).
2. Se detectaron corrupciones intencionales en el offset de datos (`0x0A`) y el tamaño de la cabecera DIB (`0x0E`), ambas suplantadas con los valores mágicos de depuración corruptos `BA D0 00 00`.
3. Se programó un script en Python utilizando la librería nativa de manipulación binaria para restaurar los valores de control estándar y reescribir el alto exacto de la imagen a 850 píxeles (`\x52\x03\x00\x00` en Little Endian).
4. El renderizado exacto alineó el bitstream original, neutralizando el desfase del lienzo y exponiendo la bandera legítima del reto en la sección superior real de la imagen.

## Flag Obtenida:
picoCTF{qu1t3_a_v13w_2020}