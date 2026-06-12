# Vigenere

## 📖 1. Descripción del Problema

El reto proporciona un mensaje cifrado utilizando el algoritmo clásico de **Vigenère** y nos entrega de forma explícita la palabra clave necesaria para revertir el proceso.

- **Texto Cifrado (Extraído de `cipher.txt`):** `rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_cc82272b}`

- **Llave Secreta:** `CYLAB`

## 🛠️ 2. Análisis y Solución Matemática

El cifrado Vigenère aplica un desplazamiento algebraico modular individual a cada letra del abecedario ($A=0, B=1, C=2, \dots$), repitiendo la palabra clave a lo largo del mensaje. Los caracteres numéricos, los guiones bajos (`_`) y las llaves (`{}`) no sufren ningún desplazamiento y se mantienen fijos.

La fórmula de descifrado para cada carácter es:

$$\text{Letra Plana} = (\text{Letra Cifrada} - \text{Letra Llave}) \pmod{26}$$

### Alineación y Descifrado Carácter por Carácter:

|**Texto Cifrado TXT**|**Letra Llave**|**Operación (Índices)**|**Letra Plana Resultante**|
|---|---|---|---|
|**`rgnoDVD`**|`CYLABCY`|Desplazamiento inicial del formato|**`picoCTF`**|
|`O`|`L`|$14 - 11 = 3$|**`D`**|
|`0`|_Ninguna_|Carácter numérico estático|**`0`**|
|`N`|`A`|$13 - 0 = 13$|**`N`**|
|`U`|`B`|$20 - 1 = 19$|**`T`**|
|`W`|`C`|$22 - 2 = 20$|**`U`**|
|`Q`|`Y`|$16 - 24 = -8 \equiv 18$|**`S`**|
|`3`|_Ninguna_|Carácter numérico estático|**`3`**|
|`G`|`L`|$6 - 11 = -5 \equiv 21$|**`V`**|
|`1`|_Ninguna_|Carácter numérico estático|**`1`**|
|`G`|`A`|$6 - 0 = 6$|**`G`**|
|`3`|_Ninguna_|Carácter numérico estático|**`3`**|
|`O`|`B`|$14 - 1 = 13$|**`N`**|
|`3`|_Ninguna_|Carácter numérico estático|**`3`**|
|`T`|`C`|$19 - 2 = 17$|**`E`**|
|`3`|_Ninguna_|Carácter numérico estático|**`3`**|
|`A`|`Y`|$0 - 24 = -24 \equiv 2$|**`C`**|
|`1`|_Ninguna_|Carácter numérico estático|**`1`**|
|`A`|`L`|$0 - 11 = -11 \equiv 15$|**`P`**|
|`H`|`A`|$7 - 0 = 7$|**`H`**|
|`3`|_Ninguna_|Carácter numérico estático|**`3`**|
|`S`|`B`|$18 - 1 = 17$|**`R`**|

### Descifrado del Hash Terminal (`cc82272b` -> `b82272z`)

- **`c`** con Llave **`B`**: $2 - 1 = 1 \rightarrow$ **`b`**

- **`82272`**: Se mantienen intactos.

- **`b`** con Llave **`C`**: $1 - 2 = -1 \equiv 25 \rightarrow$ **`z`**


##  Flag
```
picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_b82272z}
```
