# Picker II

## Descripción del Reto
Este reto de nivel intermedio (100 puntos) pertenece a la secuela directa de *Picker I*. Explora la ineficacia de las listas negras (*blacklists*) basadas en coincidencias de cadenas de texto cuando se mantiene un entorno de ejecución dinámica global activo. El objetivo consiste en evadir una función de filtrado para ejecutar código nativo de Python que vuelque el archivo secreto del servidor.

## Análisis Técnico (Blacklist Bypass & Arbitrary Python Execution)
A diferencia de la primera versión, el desarrollador implementó una función de validación intermedia para denegar el acceso a la rutina restringida `win()`:


def filter(user_input):
  if 'win' in user_input:
    return False
  return True


- **El Bloqueo**: Si la cadena ingresada por el usuario contiene la subcadena `'win'`, el filtro retorna `False`, el flujo se interrumpe y la terminal imprime `Illegal input`.

- **La Vulnerabilidad**: El programa sigue procesando la entrada válida a través de la instrucción dinámica `eval(user_input + '()')`. Dado que una lista negra solo restringe elementos específicos conocidos, no previene que un atacante inyecte sentencias completas y válidas del lenguaje de programación.

- **La Solución (Bypass)**: En lugar de invocar la función `win()`, es posible replicar su comportamiento lógico interno (`open('flag.txt').read()`) utilizando la función integrada `print()`. Para neutralizar los paréntesis vacíos `()` que el backend concatena automáticamente al final de la entrada, se añade un carácter de comentario (`#`). Esto transforma la instrucción evaluada en:

El intérprete procesa la lectura directa del archivo en el sistema de archivos local del servidor y descarta el resto de la sintaxis como un comentario plano.


## Proceso de Reconstrucción

1. Se analizó el mecanismo de control de entrada detectando que el filtro evaluaba la coincidencia estricta de la cadena de texto `'win'`.
2. Se inició una sesión persistente por red mediante sockets utilizando netcat hacia la instancia correspondiente:

 ```
  nc saturn.picoctf.net 62261
 ```


3. El backend validó la cadena como segura (al no contener la palabra prohibida), pasándola al contexto de `eval()`, el cual ejecutó el descriptor de archivo e imprimió la bandera directamente en texto plano.


## Flag Obtenida:

picoCTF{f1l73r5_f41l_c0d3_r3f4c70r_m1gh7_5ucc33d_0b5f1131}