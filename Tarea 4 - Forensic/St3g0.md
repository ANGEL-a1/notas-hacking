# St3g0

## Descripción del Reto

Este reto de nivel medio (300 puntos) pertenece a la categoría de **Forensics** y proporciona una imagen denominada:

```text
pico.flag.png
```

La descripción es muy breve:

> Download this image and find the flag.

Además, ofrece una pista muy importante:

> We know the end sequence of the message will be $t3g0.

Esta pista sugiere que existe un mensaje oculto dentro de la imagen y que conocemos su marcador final.

---

## Análisis Inicial

Al abrir la imagen se observa únicamente el logotipo de picoCTF.

No existen elementos visibles que permitan identificar una bandera:

- No hay texto oculto visible.
- No hay anomalías gráficas.
- No aparecen metadatos relevantes.
- No existen diferencias perceptibles en los colores.

Esto apunta inmediatamente a una técnica de **esteganografía**.

---

## Esteganografía LSB

La técnica más común en retos de imágenes PNG es **LSB (Least Significant Bit)**.
Cada píxel almacena información de color mediante valores binarios.

Por ejemplo:

```text
11111110
11111111
```

Visualmente ambos colores son prácticamente idénticos, pero el último bit puede utilizarse para almacenar información.

Al modificar únicamente los bits menos significativos de millones de píxeles, es posible ocultar mensajes completos sin alterar perceptiblemente la imagen.

---

## Extracción de los Bits Ocultos

Se extrajeron los bits menos significativos de los canales RGB de la imagen.

Al reconstruir los bytes ocultos apareció directamente el mensaje:

```text
picoCTF{7h3r3_15_n0_5p00n_a1062667}$t3g0
```

La secuencia final:

```text
$t3g0
```

coincide exactamente con la pista proporcionada por el reto, indicando el final del mensaje oculto.

---

## Recuperación de la Flag

El contenido extraído fue:

```text
picoCTF{7h3r3_15_n0_5p00n_a1062667}$t3g0
```

La bandera corresponde a la parte comprendida entre:

```text
picoCTF{
```

y

```text
}
```

Por lo tanto:

```text
picoCTF{7h3r3_15_n0_5p00n_a1062667}
```

---

## Flag Obtenida

```text
picoCTF{7h3r3_15_n0_5p00n_a1062667}
```