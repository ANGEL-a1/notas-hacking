# Substitution0

### Enunciado:
Un mensaje ha llegado desordenado, pero incluye la clave de sustitución en la primera línea. El objetivo es romper este cifrado de sustitución monoalfabético.[cite: 2]

---

## 🔍 Análisis Criptográfico y Solución

El reto presenta un cifrado clásico de sustitución donde cada letra del alfabeto inglés ha sido mapeada uno a uno con un alfabeto desordenado provisto como llave (Key).[cite: 2]

### 1. Datos del Desafío:
* **Llave (Key):** `OHNFUMWSVZLXEGCPTAJDYIRKQB`[cite: 2]
* **Texto Cifrado de la Flag:** `pvncNDM{5YH5717Y710G_3I0XY710G_03055505}`[cite: 2]

### 2. Mapeo Manual de la Bandera:
Analizando la estructura de la cabecera estándar de la plataforma (`picoCTF`), se deducen las sustituciones de caracteres directamente:
* `p` $\rightarrow$ `p`
* `v` $\rightarrow$ `i`
* `n` $\rightarrow$ `c`
* `c` $\rightarrow$ `o`
* `N` $\rightarrow$ `C`
* `D` $\rightarrow$ `T`
* `M` $\rightarrow$ `F`

Reemplazando el bloque ofuscado con el alfabeto de la llave se reconstruyen las palabras `SUBSTITUTION` y `EVOLUTION` manteniendo los caracteres numéricos intactos.

---

## 🏆 Flag Obtenida
**`picoCTF{5UB5717U710N_3V0LU710N_03055505}`**