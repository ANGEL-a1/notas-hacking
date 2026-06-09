# ASCII Numbers

## Descripción del Reto
Este reto de nivel medio (100 puntos) aborda el concepto de codificación de caracteres y la interpretación de datos numéricos estructurados bajo el estándar ASCII. El objetivo es tomar una secuencia de valores numéricos representados en formato hexadecimal y decodificarlos en sus caracteres alfanuméricos correspondientes para reconstruir la bandera (flag).

## Análisis de Codificación Hexadecimal y ASCII
En informática, la información de texto se almacena mediante mapeos numéricos donde cada carácter posee un valor entero asignado:
* **ASCII (American Standard Code for Information Interchange)**: Esquema de codificación que asigna valores numéricos del 0 al 127 a caracteres de control, letras, números y signos de puntuación.
* **Prefijo 0x**: Notación estándar utilizada en programación para indicar que el valor subsecuente se encuentra expresado en sistema numérico hexadecimal (base 16) en lugar de decimal (base 10). Por ejemplo, el valor hexadecimal `0x70` equivale al número decimal `112`, el cual corresponde a la letra minúscula `p` en la tabla ASCII.

## Proceso de Reconstrucción (Decodificación de Bytes)
Para resolver el desafío, se tomó la cadena de bytes provista y se procesó mediante la interpretación y conversión directa de los valores en base 16:
* Se identificó la estructura de la cadena compuesta por tokens separados por espacios, cada uno iniciando con el indicador formal de base hexadecimal `0x`.
* Se descartó el uso de herramientas web externas (como CyberChef) optando por una resolución nativa mediante un script de conversión automatizada en Python.
* Se removieron los prefijos `0x` y se transformó cada número hexadecimal a su representación entera equivalente para posteriormente mapearlo con su carácter ASCII correspondiente mediante la función `chr()`.

## Flag Obtenida:

picoCTF{45c11_n0_qu35710n5_1ll_t311_y3_n0_l135_445d4180}