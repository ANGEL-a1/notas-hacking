# RED

## Descripción del Reto

Este reto de nivel fácil (100 puntos) pertenece a la categoría de **Forensics** y proporciona una imagen llamada `red.png` que aparentemente consiste únicamente en un bloque de color rojo sólido.

La descripción y las pistas son las siguientes:

> **RED, RED, RED, RED**
> **The picture seems pure, but is it though?**
> **Red? Ged? Bed? Aed?**
> **Check whatever Facebook is called now.**

A primera vista la imagen parece completamente uniforme y no contiene ningún elemento visible que permita identificar una bandera. Sin embargo, las pistas sugieren que existe información oculta dentro del archivo.

---

## Análisis Inicial

Al abrir la imagen únicamente se observa un cuadrado rojo sin ningún detalle visible.

Esto descarta técnicas básicas como:
- Texto oculto visible.
- Cambios de contraste.
- Esteganografía visual simple.
- Metadatos evidentes.

La tercera pista:

```text
Red? Ged? Bed? Aed?
```

sugiere prestar atención a los distintos canales de color o a información almacenada a nivel de bits.

---

## Inspección de Metadatos

Durante la revisión de los metadatos PNG se encontró un bloque de texto oculto:

```text
Poem:
Crimson heart, vibrant and bold,
Hearts flutter at your sight.
Evenings glow softly red,
Cherries burst with sweet life.
Kisses linger with your warmth.
Love deep as merlot.
Scarlet leaves falling softly,
Bold in every stroke.
```

Tomando la primera letra de cada línea obtenemos:

```text
C
H
E
C
K
L
S
B
```

Lo que forma la palabra:

```text
CHECKLSB
```

Esta pista indica que debemos revisar los **Least Significant Bits (LSB)** de la imagen.

---

## Esteganografía LSB

LSB (**Least Significant Bit**) es una técnica de ocultamiento de información que aprovecha el bit menos significativo de cada píxel.

Por ejemplo:

```text
11111110
11111111
```

La diferencia visual entre ambos valores es prácticamente imperceptible para el ojo humano, pero permite almacenar información binaria oculta.

Debido a esto, es una de las técnicas más utilizadas en retos de esteganografía y análisis forense.

---

## Extracción de la Información Oculta

Tras analizar los bits menos significativos de los canales de color de la imagen se recuperó la siguiente cadena:

```text
cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==
```

La estructura de la cadena indica claramente que se encuentra codificada en **Base64**.

---

## Flag Obtenida

```text
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
```