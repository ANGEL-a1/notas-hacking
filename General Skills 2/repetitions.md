# repetitions

## Descripción del Reto
Can you make sense of this file? Download the file here.

## Solución
Para resolver este reto, analizamos el archivo `enc_flag`. El formato de la cadena de texto (especialmente el relleno `==` al final) nos indica que está codificado en Base64.
El nombre del reto y la pista sugieren una codificación anidada (múltiples capas del mismo cifrado). En lugar de decodificar a mano una por una, descargamos el archivo directo al Web Shell usando `wget` y automatizamos la decodificación encadenando comandos.

Utilizando tuberías (`|`), pasamos la salida de cada decodificación como entrada de la siguiente iteración un total de 6 veces:
`wget https://artifacts.picoctf.net/c/472/enc_flag`
`cat enc_flag | base64 -d | base64 -d | base64 -d | base64 -d | base64 -d | base64 -d`

El comando final nos revela el texto plano y la bandera.

## Bandera
`picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_73494190}`