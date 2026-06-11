# The Numbers

## Descripción del Reto
Este reto de nivel inicial (*Easy*, 50 puntos) pertenece a la categoría de Criptografía (*Cryptography*). Introduce el análisis de esteganografía textual y el uso de sistemas de sustitución numérica directa basados en el alfabeto indexado común (Cifrado A1Z26).

## Análisis Técnico (A1Z26 Substitution Cipher)
El cifrado **A1Z26** es un esquema de sustitución monoalfabético donde los caracteres del abecedario se mapean uno a uno con su correspondiente posición matemática ordinal ($A=1, B=2, \dots, Z=26$).

Forensecamente, el análisis del artefacto visual `the_numbers.png` expuso una secuencia de dígitos separados por espacios y delimitados por operadores de agrupación (`{ }`):
* Los primeros 7 números de control (`16 9 3 15 3 20 6`) corresponden exactamente a la transliteración lineal de la firma obligatoria del formato del reto: `PICOCTF`.
* Los bloques internos dentro de las llaves contienen el criptograma oculto de la sesión.

## Proceso de Reconstrucción
1. Se realizó la extracción manual de los valores numéricos inscritos sobre el canal visual del lienzo de la imagen:
   * Cabecera: `16 9 3 15 3 20 6`
   * Cuerpo interno: `20 8 5 14 21 13 2 5 18 19 13 1 19 15 14`
2. Se implementó un algoritmo en Python que itera sobre los enteros del cuerpo interno, aplicando un desplazamiento posicional sobre la tabla ASCII elemental para transformar el índice numérico a su representación de carácter alfabético:
   $$\text{Char} = \text{chr}(64 + n)$$
3. El script concatenó los strings resultantes, estructurando la bandera final en texto claro.

## Flag Obtenida:
PICOCTF{THENUMBERSMASON}