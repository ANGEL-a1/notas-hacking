# Tapping

## Descripción del Reto

Este reto de nivel medio (200 puntos) pertenece a la categoría de **Cryptography** y presenta un servicio remoto accesible mediante Netcat.

La descripción del desafío es:

> **There's tapping coming in from the wires. What's it saying?**

Además, las pistas proporcionadas son:

1. **What kind of encoding uses dashes and dots?**
    
2. **The flag is in the format PICOCTF{}**
    

Estas pistas sugieren inmediatamente el uso de **Código Morse**, un sistema de codificación basado en puntos (`.`) y rayas (`-`).

---

## Análisis Inicial

Al conectarse al servicio mediante Netcat:

```bash
nc fickle-tempest.picoctf.net 53373
```

se recibió el siguiente mensaje:

```text
.--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. ---.. -.-. ----. ----. .- ..-. .- ....- }
```

El formato coincide claramente con una secuencia codificada en Morse.

---

## Código Morse

El Código Morse representa caracteres mediante combinaciones de puntos y rayas.

Ejemplos:

|Letra|Morse|
|---|---|
|A|.-|
|B|-...|
|C|-.-.|
|P|.--.|
|I|..|
|O|---|

También existen representaciones para números:

|Número|Morse|
|---|---|
|0|-----|
|1|.----|
|2|..---|
|3|...--|
|4|....-|
|8|---..|
|9|----.|

---

## Decodificación

Separando cada grupo Morse y traduciéndolo:

```text
.--.      P
..        I
-.-.      C
---       O
-.-.      C
-         T
..-.      F
```

Se obtiene:

```text
PICOCTF
```

Continuando con el contenido dentro de las llaves:

```text
--       M
-----    0
.-.      R
...      S
...--    3
-.-.     C
-----    0
-..      D
...--    3
.----    1
...      S
..-.     F
..-      U
-.       N
---..    8
-.-.     C
----.    9
----.    9
.-       A
..-.     F
.-       A
....-    4
```

Resultado:

```text
M0RS3C0D31SFUN8C99AFA4
```

---

## Reconstrucción de la Bandera

Uniendo el prefijo y el contenido decodificado:

```text
picoCTF{M0RS3C0D31SFUN8C99AFA4}
```

---
## Flag Obtenida

```text
picoCTF{M0RS3C0D31SFUN8C99AFA4}
```