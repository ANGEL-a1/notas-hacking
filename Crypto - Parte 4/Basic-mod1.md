# basic-mod1

## Descripción del Reto
Este reto de nivel medio (100 puntos) pertenece a la categoría de Criptografía y consiste en la implementación de un esquema de descifrado basado en aritmética modular y sustitución monoalfabética. El objetivo es procesar una lista de valores numéricos enteros, aplicarles una reducción cíclica bajo un módulo específico ($x \pmod{37}$) y mapear los residuos resultantes hacia un conjunto de caracteres alfanuméricos predefinido para reconstruir el mensaje oculto.

## Análisis de Aritmética Modular y Mapeo Criptográfico
La aritmética modular es un sistema aritmético para clases de equivalencia de números enteros, donde los números "dan la vuelta" al alcanzar un cierto valor fijo denominado **módulo**.
* **Operación Módulo ($n \pmod m$)**: Matemáticamente, devuelve el residuo o remanente de la división entera de $n$ entre $m$. Por ejemplo, $350 \div 37 = 9$ con un residuo de $17$. Por lo tanto, $350 \pmod{37} = 17$.
* **Conjunto de Caracteres (Character Set)**: El espacio de búsqueda de soluciones se reduce a 37 posibles estados de residuos ($0$ a $36$), divididos en tres subgrupos de conversión:
  * Rangos $[0 - 25] \rightarrow$ Letras del alfabeto en mayúsculas ($\text{A} - \text{Z}$).
  * Rangos $[26 - 35] \rightarrow$ Dígitos decimales ($0 - 9$).
  * Estado $[36] \rightarrow$ Carácter especial guion bajo (`_`).

## Proceso de Reconstrucción (Automatización en Python)
Dado que el archivo `message.txt` contenía una ráfaga masiva de valores numéricos, se descartó el cálculo analítico manual y se desarrolló un script de automatización en Python empleando manipulación de vectores y conversión de códigos ASCII (`chr()`):
* Se parseó la lista de enteros dentro de una estructura de datos indexada.
* Se iteró sobre cada elemento aplicando el operador aritmético `% 37`.
* Se implementaron condicionales lógicos para desviar el residuo obtenido hacia su equivalente ASCII correspondiente (sumando el desplazamiento base `65` para mayúsculas y ajustando para los dígitos numéricos).
* Los caracteres resultantes se concatenaron y se envolvieron dentro de la estructura formal del formato de banderas de la competencia.

## Flag Obtenida:

picoCTF{R0UND_N_R0UND_ADD17EC2}