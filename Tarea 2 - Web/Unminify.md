# Unminify

## Descripción del Reto
Este reto de nivel fácil (100 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Explora el concepto de minificación de código fuente y aborda la falsa percepción de seguridad (*Security through obscurity*) que ocurre cuando se asume que compactar el código en texto plano impide el análisis de datos sensibles por parte del cliente.

## Análisis Técnico (Code Minification vs Obfuscation)
La minificación es una técnica de optimización que elimina de forma automatizada los caracteres prescindibles de un archivo (espacios, saltos de línea, comentarios y tabulaciones) con el único fin de reducir el tamaño del recurso y acelerar los tiempos de transferencia HTTP/S en la red.

* **La Vulnerabilidad**: Un error recurrente en el desarrollo web consiste en confundir la minificación con la ofuscación o el cifrado. Debido a que el código minificado se agrupa en una única línea masiva y carece de formato legible, los desarrolladores asumen que los elementos incrustados se vuelven invisibles. No obstante, dado que el documento HTML sigue transmitiéndose en texto plano para su interpretación en el DOM, la estructura completa permanece intacta y expuesta a auditorías directas mediante la lectura del código fuente original.
* **La Solución**: Forzar el despliegue del código base transferido por el servidor web omitiendo las reglas de renderizado visual del navegador.

## Proceso de Reconstrucción
1. Se accedió a la interfaz web expuesta por la instancia activa del reto.
2. Al procesar la indicación del portal que afirmaba que el navegador ya albergaba la bandera localmente, se procedió a invocar el comando `Ctrl + U` para examinar el código fuente sin procesar.
3. Se observó que el archivo HTML se encontraba compactado en una sola línea de texto plano desprovista de formateo estructural.
4. Se utilizó el motor de búsqueda nativo del navegador (`Ctrl + F`) bajo la palabra clave `picoCTF`.
5. Se identificó que la bandera del sistema se encontraba embebida directamente dentro de las propiedades de estilo del documento, específicamente declarada de forma errónea como el identificador de clase de una etiqueta de párrafo:

## Flag Obtenida:

picoCTF{pr3tty_c0d3_b99eb82e}