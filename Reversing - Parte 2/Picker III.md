# Picker III

## Descripción del Reto
Este reto de nivel intermedio (100 puntos) pertenece a la categoría de Ingeniería Inversa (*Reverse Engineering*) y cierra la trilogía de *Picker*. Explora vulnerabilidades de corrupción de memoria lógica y manipulación de variables globales en Python para evadir un sistema de control de flujo basado en una tabla estática de funciones permitidas.

## Análisis Técnico (Function Table Corruption & Arbitrary Variable Write)
En esta versión, el desarrollador intentó restringir la ejecución arbitraria eliminando la entrada libre al comando `eval()`. En su lugar, implementó una tabla de funciones predefinidas en una variable de texto global llamada `func_table`:


func_table = \
'''\
print_table                     \
read_variable                   \
write_variable                  \
getRandomNumber                 \
'''

Cada una de las 4 funciones permitidas tiene asignado un bloque estático de exactamente 32 bytes (`FUNC_TABLE_ENTRY_SIZE`). Cuando el usuario elige ejecutar una opción del menú (1-4), el programa calcula el desplazamiento en la cadena, extrae el nombre de la función y la invoca mediante `eval(func_name + '()')`.

- **La Vulnerabilidad**: El programa expone la función `write_variable()`, la cual utiliza la instrucción dinámica `exec('global '+var_name+'; '+var_name+' = '+value)` sin una lista restrictiva de variables protegidas. Esto otorga capacidades de escritura arbitraria en el espacio de nombres global.

- **La Explotación (Bypass)**: Un atacante puede invocar `write_variable` apuntando directamente hacia la variable `func_table`. Al reescribir esta cadena, se puede suplantar la cuarta entrada (`getRandomNumber`) por el identificador de la función restringida `win`. Para evitar romper la consistencia del script y disparar el mensaje `Table corrupted`, se debe asegurar que la longitud total de la nueva cadena sea de exactamente 128 bytes (32×4), rellenando los espacios vacíos con caracteres nulos o espacios en blanco.


## Proceso de Reconstrucción

1. Se analizó el código fuente identificando que `write_variable` permitía modificar cualquier variable global del entorno en ejecución.

2. Se estableció una conexión persistente por red mediante sockets utilizando netcat hacia el servidor del reto:

```
nc saturn.picoctf.net 58802
```

3. En el prompt interactivo, se seleccionó la opción **`3`** (`write_variable`).

4. Al solicitar el nombre de la variable, se ingresó: `func_table`.

5. Al solicitar el valor, se inyectó la tabla modificada manteniendo la estructura simétrica de 32 bytes por bloque, reemplazando la última función por `win`:


```
   "print_table                     read_variable                   write_variable                 win                             "
```

6. Finalmente, se seleccionó la opción **`4`** del menú principal. El backend extrajo la cadena `win` de la cuarta ranura de memoria modificada y la ejecutó, devolviendo la bandera codificada en formato hexadecimal.

## Flag Obtenida:

picoCTF{7h15_15_wh47_w3_g37_w17h_u53r5_1n_ch4rg3_226dd285}
