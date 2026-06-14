# Substitution2

### Descripción

Se interceptó un nuevo mensaje cifrado mediante un esquema de sustitución monoalfabética. A diferencia del reto anterior, el atacante eliminó todos los signos de puntuación y espacios para dificultar el análisis de frecuencia. El objetivo es recuperar el mensaje original y obtener la bandera.

---

## Análisis Criptográfico y Solución

El archivo proporcionado contiene un texto extenso cifrado mediante una sustitución monoalfabética. Debido a la ausencia de espacios y puntuación, un análisis de frecuencia simple resulta insuficiente, por lo que fue necesario estudiar patrones de letras repetidas, bigramas y trigramas.

### 1. Datos del Desafío:

- **Texto Cifrado:** Cadena continua de caracteres alfabéticos sin separación de palabras.

- **Pista del reto:** Analizar grupos de letras para mejorar el ataque de frecuencia.


### 2. Proceso de Descifrado:

Se aplicó un ataque de frecuencia considerando:

- Frecuencia de letras individuales.

- Patrones repetitivos dentro del texto.

- Bigramas y trigramas comunes del idioma inglés.

- Estructura típica de las banderas de picoCTF.


Al descifrar el mensaje completo se observó que la bandera aparecía al final del texto. Inicialmente se identificó una cadena parcialmente descifrada:

`UIE{K6F4G_4K41R515_15_73A10B5_702E03EU}`

A partir de la clave de sustitución recuperada, cada símbolo pudo ser traducido correctamente obteniendo:

- `K6F4G` → `NGRAM`
- `4K41R515` → `ANALYSIS`
- `15` → `IS`
- `73A10B5` → `TEDIOUS`
- `702E03EU` → `TODECODE`

La frase completa resultante fue:

`NGRAM_ANALYSIS_IS_TEDIOUS_TODECODE`

---

## 🏆 Flag Obtenida

**`picoCTF{N6R4M_4N41Y515_15_73D10U5_702F03FC}`**