# Secret of the Polyglot

## Descripción del Reto

Este reto de nivel fácil (100 puntos) pertenece a la categoría de **Forensics** y proporciona un archivo denominado:

```text
flag2of2-final.pdf
```

La descripción indica que el NOC (Network Operations Center) ha encontrado un archivo sospechoso que produce resultados contradictorios al intentar identificar su tipo.

La pista principal es:

> This problem can be solved by just opening the file in different ways.

Esto sugiere que el archivo puede contener más de un formato válido simultáneamente.

---

## ¿Qué es un Archivo Políglota?

Un archivo políglota es un archivo diseñado para ser interpretado correctamente por más de un tipo de programa.

Por ejemplo:

- Un archivo que funciona como PDF y PNG al mismo tiempo.
- Un archivo que es válido tanto como ZIP como HTML.
- Un archivo que puede ser ejecutable y documento simultáneamente.

Este tipo de técnicas son frecuentes en retos forenses y en investigaciones de malware.

---

## Análisis Inicial

El archivo fue entregado con extensión:

```text
flag2of2-final.pdf
```

Al abrirlo normalmente como PDF se observó únicamente una parte de la bandera.

Contenido encontrado:

```text
1n_pn9_&_pdf_7f9bccd1}
```

Claramente no corresponde a una flag completa.

---

## Inspección del Encabezado

Al revisar los primeros bytes del archivo se descubrió que realmente comenzaba con la firma de un archivo PNG:

```text
89 50 4E 47
```

equivalente a:

```text
PNG
```

Esto confirmó que el archivo también era una imagen válida.

---

## Apertura como Imagen

Al abrir el mismo archivo utilizando un visor de imágenes o renombrándolo con extensión `.png`, apareció texto adicional.

Contenido recuperado:

```text
picoCTF{f1u3n7_
```

---

## Reconstrucción de la Bandera

Primera parte (PNG):

```text
picoCTF{f1u3n7_
```

Segunda parte (PDF):

```text
1n_pn9_&_pdf_7f9bccd1}
```

Bandera completa:

```text
picoCTF{f1u3n7_1n_pn9_&_pdf_7f9bccd1}
```
---

## Flag Obtenida

```text
picoCTF{f1u3n7_1n_pn9_&_pdf_7f9bccd1}
```