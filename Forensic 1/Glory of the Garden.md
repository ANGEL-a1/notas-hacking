# Glory of the Garden

## Descripción del Reto
Este reto introductorio (50 puntos) pertenece a la categoría de Forense Computacional y aborda el análisis de datos remanentes e inyecciones de texto plano en contenedores multimedia. El desafío proporciona una imagen legítima en formato JPEG (`garden.jpg`). El objetivo es inspeccionar el archivo binario más allá de sus marcadores estructurales estándar para extraer una bandera oculta en los sectores de datos no interpretados por el renderizador gráfico.

## Análisis de Estructuras JPEG e Inyección de Criptogramas
El formato JPEG define una arquitectura de marcadores específicos en hexadecimal para delimitar el flujo de datos:
* `FF D8`: Identifica el inicio físico del archivo (*Start of Image*).
* `FF D9`: Identifica la terminación formal de la matriz gráfica (*End of Image*).

Los visores de imágenes detienen la lectura del archivo al procesar el marcador `FF D9`. Cualquier información o cadena de caracteres ASCII concatenada con posterioridad a este offset permanece oculta para la interfaz de usuario, pero es completamente accesible mediante análisis estático de cadenas (*Strings Analysis*) o inspección hexadecimal.

## Proceso de Reconstrucción
* **Validación**: Se inspeccionó el archivo binario para identificar cadenas legibles que cumplieran con la sintaxis del objetivo basándose en metodologías de análisis estático.
* **Extracción**: Se ejecutó un filtrado de flujos binarios mediante un script automatizado en Python que localizó el offset del byte `FF D9` y extrajo el payload residual:

# Flag

`picoCTF{more_than_m33ts_the_3y339cbe6dc}`