# Bookmarklet

## Descripción del Reto
Este reto introductorio (50 puntos) pertenece a la categoría de Explotación Web y demuestra el uso de *Bookmarklets* (marcadores dinámicos) para ejecutar lógica de scripting en el entorno del cliente (*Client-Side Execution*). El portal proporciona un script de JavaScript ofuscado encargado de descifrar localmente una bandera que ya ha sido entregada en el DOM.

## Análisis Técnico y Desafíos de Codificación
Un bookmarklet es un marcador convencional cuyo URI utiliza el esquema `javascript:` para invocar al motor de scripting del navegador sobre el contexto de la página web actual. 

* **El Problema del Encoding**: Al intentar extraer o replicar la lógica del script fuera del navegador (como entornos locales de Python o terminales de Windows), la cadena cifrada cruda (`"àÒÆÞ¦È¬ëÙ£Ö—ÓÚåÛÑ¢ÕÓœÒËÉ§œ©™í"`) suele sufrir alteraciones. Esto ocurre porque contiene caracteres no ASCII e invisibles (como bytes de control/desbordamiento) que mutan según el mapa de caracteres (*encoding*) activo del portapapeles o de la consola, corrompiendo el cálculo matemático de la resta ASCII con la clave `"picoctf"`.
* **Solución de Auditoría**: La forma más limpia y estándar en auditorías web consiste en forzar la ejecución del script utilizando el motor nativo del navegador (V8) a través de la consola de desarrollador (*DevTools*), garantizando la integridad exacta de los bytes en memoria.

## Proceso de Reconstrucción
1. Se identificó la función anónima autoinvocada expuesta en el recuadro del reto.
2. Se extrajo el script y se adaptó para su ejecución directa en la consola de depuración global de Opera GX eliminando el protocolo inicial `javascript:`.
3. El motor del navegador procesó de forma nativa la matriz de bytes del ciclo, arrojando el texto plano correcto de la contraseña sin colisiones de formatos.

## Flag Obtenida:
picoCTF{p@g3_turn3r_6bbf8953}