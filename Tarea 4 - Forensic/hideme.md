# hideme

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 100 puntos) pertenece a la categoría de Análisis Forense (*Forensics*). Desarrolla conceptos de análisis de estructuras híbridas en archivos multimedia y técnicas de ocultamiento de datos basados en la inyección de sistemas de archivos comprimidos al final del archivo contenedor (*End-of-File Data Appending*).

## Análisis Técnico (PNG File Anatomy & Concatenated Archives)
Los archivos de imagen bajo el estándar PNG poseen una estructura binaria estrictamente tipada. El archivo debe iniciar obligatoriamente con la firma de 8 bytes de cabecera (`\x89PNG\r\n\x1a\n`) y concluir de forma síncrona con el marcador de finalización del bloque crítico de renderizado llamado **`IEND`** (`\x49\x45\x4e\x44\xae\x42\x60\x82`).

* **Ocultamiento por EOF (End of File)**: Las herramientas de esteganografía superficial aprovechan que los visualizadores de imágenes detienen la lectura binaria inmediatamente después de encontrar el marcador de cierre `IEND`. Cualquier flujo de bytes concatenado de forma posterior es ignorado por el renderizador del sistema operativo.
* **Archivos Políglotas**: En este reto, se inyectó un archivo comprimido tipo `.zip` (identificable forensicamente por la firma mágica `PK\x03\x04` en sus bytes iniciales) justo detrás de la firma `IEND`.

## Proceso de Reconstrucción
1. Se recuperó el artefacto multimedia sospechoso transmitido por la red (`flag (1).png`).
2. Se programó un script en Python nativo para analizar los límites binarios del contenedor:
   * Localizó el offset exacto de la firma del bloque crítico `IEND`.
   * Realizó un corte de datos (*Carving*) aislando los 3,191 bytes adicionales que se encontraban concatenados en la cola del archivo.
3. El script validó la firma mágica `PK\x03\x04` y guardó de forma automatizada dicho flujo como un archivo comprimido válido (`oculto.zip`).
4. Al desempaquetar el buffer mediante el módulo integrado `zipfile`, se extrajo de forma recursiva un árbol de directorios oculto que contenía la ruta `secret/flag.png`.
5. Se procedió a la apertura visual del lienzo multimedia extraído, revelando la bandera del reto en texto plano.

## Flag Obtenida:
picoCTF{Hiddinng_An_imag3_within_@n_ima9e_cda72af0}