# CanYouSee

## Descripción del Reto
Este reto de nivel inicial (*Easy*, 100 puntos) pertenece a la categoría de Análisis Forense (*Forensics*). Desarrolla habilidades de auditoría sobre metadatos avanzados incrustados en contenedores multimedia JPEG, específicamente el análisis de esquemas Adobe XMP (*Extensible Metadata Platform*) y la decodificación de payloads ocultos mediante codificación Base64.

## Análisis Técnico (XMP Metadata Structure)
Además de las etiquetas Exif convencionales, las imágenes modernas suelen incluir bloques de metadatos estructurados bajo el estándar **XMP (Extensible Metadata Platform)** de Adobe, usualmente envueltos en un esquema XML legible (`<?xpacket...?>`).

En este escenario forense:
* La firma de la bandera no fue inyectada en los campos comunes de la cámara, sino dentro del nodo de licencias de Creative Commons (`cc:attributionURL`).
* Para evadir firmas de cadenas simples y el comando básico `strings`, el flag se ofuscó codificándolo en **Base64**. El análisis requirió aislar el flujo del archivo binario y localizar el namespace `http://ns.adobe.com/xap/1.0/` para extraer el string representativo.

## Proceso de Reconstrucción
1. Se descargó el artefacto multimedia del reto (`ukn_reality.jpg`), el cual corresponde a una fotografía digital.
2. Al no contar con utilidades externas instaladas en el entorno local, se programó un script en Python para escanear de forma nativa los bloques binarios legibles en la cabecera del archivo.
3. El script expuso el contenedor XML de Adobe XMP procesado por la herramienta `Image::ExifTool`.
4. Se detectó el atributo sospechoso:

   <cc:attributionURL rdf:resource='cGljb0NURntNRTc0RDQ3QV9ISUREM05fM2I5MjA5YTJ9Cg=='/>


5. Al aislar la cadena y aplicarle una decodificación Base64 inversa, se obtuvo la bandera en texto plano.

## Flag Obtenida:

picoCTF{ME74D47A_HIDD3N_3b9209a2}