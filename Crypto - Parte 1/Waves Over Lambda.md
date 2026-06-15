# Waves Over Lambda

## Descripción

Se nos proporciona un texto aparentemente cifrado mediante múltiples sustituciones y una pista implícita en el título:

```text
waves over lambda
```

El objetivo es recuperar el mensaje original y obtener la bandera.

**Categoría:** Cryptography  
**Dificultad:** Medium

---

## Texto Cifrado

Al iniciar la instancia se muestra:

```text
bvgqaljf ipap hf kvda rylq - rapedpgbk_hf_b_vcpa_ylmsol_8003r343
```

seguido de un bloque largo de texto cifrado.

A simple vista puede observarse que:

- Los espacios se conservan.
    
- La longitud de las palabras coincide con texto en inglés.
    
- La distribución de caracteres parece seguir frecuencias normales del idioma.
    

Esto sugiere un **cifrado por sustitución monoalfabética**.

---

## Análisis

El comienzo del texto cifrado es:

```text
ilchgq ilo fvmp jhmp lj mk ohfwvfly
```

Tras analizar frecuencias y patrones comunes del inglés se identifica como:

```text
during the some time at my disposal
```

Continuando con el análisis se observa que el texto completo corresponde al famoso párrafo inicial de:

```text
Dracula
```

de Bram Stoker.

Fragmento original:

```text
I had for some time at my disposal...
```

Al disponer del texto conocido (known plaintext), resulta sencillo reconstruir la tabla de sustitución utilizada.

---

## Descifrado

Aplicando la sustitución inversa al mensaje inicial:

```text
bvgqaljf ipap hf kvda rylq
```

se obtiene:

```text
congrats here is your flag
```

y la cadena:

```text
rapedpgbk_hf_b_vcpa_ylmsol_8003r343
```

se transforma en:

```text
frequency_is_c_over_lambda_8003f343
```

---

## Explicación del Título

El nombre del reto:

```text
waves over lambda
```

hace referencia a la ecuación fundamental de ondas:

f=\frac{c}{\lambda}

donde:

- **f** = frecuencia
    
- **c** = velocidad de propagación
    
- **λ** = longitud de onda
    

Por eso la bandera contiene:

```text
frequency_is_c_over_lambda
```

---

## Flag

```text
frequency_is_c_over_lambda_8003f343
```

---

## Lecciones Aprendidas

- Los cifrados de sustitución monoalfabética son vulnerables al análisis de frecuencia.
    
- Reconocer textos históricos o literarios puede acelerar enormemente la resolución.
    
- Los ataques de **known plaintext** permiten reconstruir rápidamente alfabetos de sustitución.
    
- Los títulos de los retos suelen contener pistas importantes sobre la solución.
    

## Concepto Criptográfico

**Monoalphabetic Substitution Cipher**

Cada letra del texto original es reemplazada por otra letra fija del alfabeto. Aunque sencillo de implementar, este esquema es fácilmente rompible mediante:

- análisis de frecuencia,
    
- patrones de palabras,
    
- coincidencia con textos conocidos,
    
- ataques de texto conocido (known plaintext).