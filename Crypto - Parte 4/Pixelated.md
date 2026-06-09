# Pixelated

## Descripción del Reto
Este reto de nivel medio (200 puntos) pertenece a la categoría de Criptografía y aborda el concepto de **Criptografía Visual** (Visual Cryptography Scheme o VCS). El desafío proporciona dos imágenes de ruido pseudoaleatorio en formato PNG (`scrambled1.png` y `scrambled2.png`). El objetivo es descifrar el secreto compartido superponiendo o combinando algebraicamente las matrices de píxeles de ambas imágenes contenedoras para hacer emerger la bandera oculta.

## Análisis de Criptografía Visual
La criptografía visual es una técnica criptográfica que permite descifrar mensajes visuales sin necesidad de realizar cálculos complejos de computadora, simplemente superponiendo transparencias físicas. 
* **Secreto Compartido (Secret Sharing)**: Una imagen original se descompone en $n$ piezas llamadas "sombras" o "capas". Ninguna capa por separado revela información sobre el secreto original.
* **Mecanismo Digital**: En entornos digitales, las operaciones aritméticas de matrices como la suma modular ($\text{Píxel}_1 + \text{Píxel}_2 \pmod{256}$) actúan como el equivalente físico de encimar dos acetatos transparentes, cancelando el ruido de fase y revelando los contornos de los caracteres ocultos.

## Proceso de Reconstrucción (Combinación de Matrices)
Para resolver la vulnerabilidad visual, se implementó un script de automatización en Python empleando procesamiento matricial de imágenes:
* Se vectorizaron las estructuras de datos bidimensionales de los archivos `scrambled1.png` y `scrambled2.png` convirtiéndolas a arreglos de tipo `uint8` en NumPy.
* Se ejecutó una suma aritmética elemento a elemento de los canales RGB de ambas fuentes. El desbordamiento natural de los enteros de 8 bits realiza la operación módulo 256 de forma nativa, rompiendo la entropía visual del ruido.

## Flag Obtenida:

picoCTF{8cdf93c3}