# Redaction gone wrong

## Descripción del Reto

Este reto de nivel medio (100 puntos) pertenece a la categoría de **Forensics** y proporciona un documento PDF denominado `Financial_Report_for_ABC_Labs.pdf`.

La premisa del desafío es identificar información sensible que supuestamente fue ocultada mediante redacción (redaction). Sin embargo, la pista principal indica que parte de la información no fue eliminada correctamente:

> **Now you DON’T see me.**

Además, el reto plantea la siguiente pregunta:

> **Can you find an important key that was not redacted properly?**

La misión consiste en verificar si la información censurada fue realmente eliminada o simplemente ocultada visualmente.

---

## Concepto de Redacción de Documentos

La redacción (redaction) es el proceso mediante el cual se elimina información sensible de un documento antes de compartirlo.

Una redacción correcta:

- Elimina permanentemente el contenido original.
- Impide recuperar la información mediante selección de texto.
- No deja datos ocultos en capas internas del documento.

Una redacción incorrecta:

- Simplemente coloca un rectángulo negro encima del texto.
- Mantiene el contenido original dentro del PDF.
- Permite recuperar la información mediante extracción o copia del texto.

Este error es extremadamente común en documentos corporativos y gubernamentales.

---

## Análisis del PDF

Al abrir el documento se observan varias secciones aparentemente censuradas.

Sin embargo, al inspeccionar el contenido interno del PDF mediante extracción de texto, se recuperó la información oculta que seguía almacenada debajo de la capa negra.

El texto extraído contenía:

```text
Financial Report for ABC Labs, Kigali, Rwanda for the year 2021.
Breakdown - Just painted over in MS word.

Cost Benefit Analysis
Credit Debit
This is not the flag, keep looking
Expenses from the
picoCTF{C4n_Y0u_S33_m3_fully}
Redacted document.
```

---

## Identificación de la Bandera

Dentro del contenido oculto aparece directamente la bandera:

```text
picoCTF{C4n_Y0u_S33_m3_fully}
```

Esta información permanecía accesible porque el texto nunca fue eliminado del PDF; únicamente fue cubierto visualmente.

---

## Procedimiento Utilizado

### 1. Inspección del Documento

Se abrió el PDF y se identificaron las áreas aparentemente redactadas.

### 2. Extracción del Texto

Se utilizó la capacidad de selección o extracción de texto del PDF para revelar el contenido oculto.

Herramientas posibles:

```bash
pdftotext Financial_Report_for_ABC_Labs.pdf
```

o simplemente:

- Copiar y pegar el contenido.

- Seleccionar texto debajo de las áreas negras.

- Utilizar lectores PDF que permitan exportar texto.

### 3. Recuperación de Información Oculta

La extracción reveló que la redacción había sido realizada únicamente mediante superposición gráfica, manteniendo el texto original intacto.

### 4. Obtención de la Bandera

Entre los datos ocultos se encontró la flag del reto.


---

## Flag Obtenida

```text
picoCTF{C4n_Y0u_S33_m3_fully}
```