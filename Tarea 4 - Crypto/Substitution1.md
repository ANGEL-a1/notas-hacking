# Substitution1

### Enunciado:
Un segundo mensaje ha llegado descifrado bajo un esquema de sustitución monoalfabética. El objetivo es romper el cifrado analizando la frecuencia de las palabras y la estructura del flag.

---

## 🔍 Análisis Criptográfico y Solución

El reto presenta un texto cifrado donde las letras del alfabeto fueron mapeadas uno a uno. La bandera se encuentra expuesta al final del payload.

### 1. Datos del Desafío:
* **Texto Cifrado del Flag:** `cbzjZWD{DF3LP3VZS_4774ZN5_4F3_Z001_4871X6DT}`

### 2. Proceso de Descifrado:
Utilizando el formato conocido de la plataforma `picoCTF` se infieren las primeras sustituciones (`ZWD` $\rightarrow$ `CTF`). Analizando el resto de las palabras comunes del párrafo (`wex` $\rightarrow$ `the`, `dqar` $\rightarrow$ `flag`), se recupera el mensaje en Leet Speak.

El reto introduce una colisión visual en la palabra `COOL`, empleando una letra `l` (L minúscula) en lugar de un número `1`, junto con un mapeo estricto para el hash final:
* `DF3LP3VZS` $\rightarrow$ `FR3QU3NCY`
* `4774ZN5` $\rightarrow$ `4774CK5`
* `4F3` $\rightarrow$ `4R3`
* `Z00l` $\rightarrow$ `C00l` (Uso de L minúscula)
* `4871X6DT` $\rightarrow$ `4871E6FB`

---

## 🏆 Flag Obtenida
**`picoCTF{FR3QU3NCY_4774CK5_4R3_C00l_4871E6FB}`**