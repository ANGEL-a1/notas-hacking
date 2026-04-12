# MatchTheRegex

## Descripción del Reto
How about trying to match a regular expression. El reto consiste en encontrar una cadena de texto que cumpla con el patrón definido en el script de validación de la página.

## Solución
Al inspeccionar el código fuente de la página, se encontró una función de JavaScript llamada `send_request()`. Dentro de esta función, un comentario revelaba la expresión regular esperada por el servidor: `^p.....F!?`.

Análisis del Regex:
- `^p`: Debe comenzar con la letra 'p'.
- `.....`: Debe contener 5 caracteres adicionales.
- `F`: Debe terminar con una 'F'.

Al ingresar la palabra `picoCTF` en el campo de texto, el sistema valida la entrada mediante una solicitud `fetch` y retorna la bandera en un cuadro de alerta.

## Bandera
`picoCTF{succ3ssfully_matchtheregex_8ad436ed}`