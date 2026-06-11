# Easy1

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 100 puntos) pertenece a la categoría de Criptografía (*Cryptography*). Introduce el funcionamiento de los sistemas de cifrado polialfabéticos simétricos mediante el uso guiado de una Tabula Recta o Matriz de Vigenère.

## Análisis Técnico (Vigenère Cipher Mechanics)
A diferencia del Cifrado César (que aplica un único desplazamiento estático a todo el documento), el cifrado de **Vigenère** utiliza una llave textual para alterar el parámetro de desplazamiento en cada carácter secuencial. 

El flujo matemático se rige bajo la aritmética modular de base 26 (longitud del alfabeto latino internacional):
$$\text{Descifrado}(C_i) = (C_i - K_i) \pmod{26}$$

Donde:
* $C_i$ es el índice decimal del carácter cifrado actual ($A=0, B=1, \dots$).
* $K_i$ es el índice decimal del carácter de la clave homóloga.

Para el reto se proporcionaron las estructuras estáticas:
* $\text{Criptograma (C)} = \text{UFJKXQZQUNB}$
* $\text{Llave (K)} = \text{SOLVECRYPTO}$

## Proceso de Reconstrucción
1. Se analizaron las dimensiones simétricas de la llave y el criptograma (ambos de longitud de 11 caracteres).
2. Se implementó un algoritmo en Python que realiza la sustracción modular de los índices ASCII de los caracteres en paralelo empleando la función interna `zip()`.
3. El script normalizó los resultados desplazando los enteros de vuelta al bloque alfabético de mayúsculas (`ord('A')`), decodificando la frase oculta *'CRYPTOISFUN'*.

## Flag Obtenida:
picoCTF{CRYPTOISFUN}