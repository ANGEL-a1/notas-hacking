# c0rrupt

## Enunciado
El desafío proporciona un archivo binario corrupto (`mystery`). El objetivo es identificar el formato original, reparar sus bytes estructurales dañados y recuperar la bandera.
## Análisis y Solución

1. **Identificación del Formato:** Al abrir el archivo binario, la presencia de metadatos como `sRGB`, `gAMA` y `pHYs` evidencian que el archivo original corresponde a una imagen en formato PNG cuyas cabeceras fueron alteradas intencionalmente
2. **Reparación Hexadecimal:** Utilizando un editor hexadecimal, se restauraron los valores estándar de la especificación PNG:
   - **Firma del archivo:** Se corrigieron los primeros bytes corruptos `89 65 4E 34` a `89 50 4E 47 0D 0A 1A 0A` (`‰PNG`)
   - **Chunk IHDR:** Se modificó la firma errónea `C"DR` por `49 48 44 52` (`IHDR`)
   - **Chunk IDAT:** Se corrigió la cabecera de datos de `DETx` a `49 44 41 54` (`IDAT`)
1. **Visualización:** Tras guardar el archivo con la extensión `.png`, la estructura se vuelve válida y el visor despliega la imagen que contiene la flag en texto plano.

## Bandera
** Flag:** `picoCTF{c0rrupt10n_1847995}`