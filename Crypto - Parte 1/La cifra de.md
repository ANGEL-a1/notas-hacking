# La cifra de

## Descripción

Se nos proporciona un texto cifrado junto con una pista bastante importante:

> "Perhaps looking at history will help"

El objetivo es descifrar el mensaje y recuperar la bandera oculta.

**Categoría:** Cryptography  
**Dificultad:** Medium

---

## Análisis Inicial

Al conectarnos al servicio obtenemos un largo texto cifrado:

```text
Ne iy nytkwpsznyg nth it mtsztcy...
```

Entre el texto aparece algo que parece una bandera parcialmente legible:

```text
CZK{m311a50_0x_a1rn3x3_h1ah3xfL83Bg7G}
```

Esto indica que probablemente estamos ante un cifrado clásico de sustitución o polialfabético.

---

## Pista Clave

El reto proporciona la siguiente pista:

```text
Perhaps looking at history will help
```

Leyendo el texto cifrado se observan nombres históricos extraños como:

```text
Bnretèwp Cousex
Volpnèxj
```

Tras intentar identificar el contenido, se descubre que el texto describe la historia del:

```text
Vigenère Cipher
```

y menciona personajes históricos relacionados con dicho cifrado.

Esto sugiere fuertemente que el texto está cifrado usando un cifrado de Vigenère.

---

## Descifrado

Utilizando herramientas de análisis de Vigenère (como CyberChef, dCode o quipqiup) se puede identificar la clave adecuada y descifrar completamente el texto.

Una vez descifrado aparece la bandera:

## Flag

```text
picoCTF{b311a50_0r_v1gn3r3_c1ph3raA83Ba7B}
```

---

## Lecciones Aprendidas

- Reconocer referencias históricas puede revelar el tipo de cifrado utilizado.
    
- El cifrado de Vigenère es un cifrado polialfabético clásico.
    
- Herramientas como CyberChef y dCode simplifican enormemente el análisis de cifrados históricos.
    
- Las pistas del reto suelen indicar indirectamente la técnica necesaria para resolverlo.
    

## Herramientas Utilizadas

- CyberChef
    
- dCode Vigenère Cipher Solver
    
- Análisis de frecuencia
    
- Reconocimiento de contexto histórico
    

## Vulnerabilidad / Concepto

**Vigenère Cipher Cryptanalysis**

El reto consistía en identificar que el texto estaba cifrado mediante Vigenère y utilizar técnicas de criptoanálisis clásico para recuperar el mensaje original y la bandera.