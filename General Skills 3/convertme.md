# Convertme 

## Descripción del Reto
Este reto nos presenta un script interactivo en Python (convertme.py) que solicita al usuario realizar una conversión numérica de base decimal a base binaria sobre un entero aleatorio. El objetivo es realizar un análisis estático sobre el código fuente para eludir la validación interactiva y descifrar la cadena de texto protegida, la cual corresponde a la bandera (flag) del reto.

Al revisar el script, observamos que el programa implementa las siguientes mecánicas:

1. Selecciona un número entero pseudoaleatorio en un rango de 10 a 100 mediante `random.choice(range(10,101))`.
2. Solicita una entrada por consola (`input()`) esperando recibir el equivalente binario exacto de dicho número.
3. Si la validación es exitosa (`ans_num == num`), el programa invoca de forma interna la función `str_xor(flag_enc, 'enkidu')` para revelar la bandera oculta.

Proceso de Reconstrucción (Bypass Estático)
Para resolverlo, se aplicó ingeniería inversa básica aislando los elementos estáticos (hardcoded) del archivo original. Debido a que tanto el arreglo binario cifrado (`flag_enc`) como la clave simétrica (`enkidu`) se encuentran fijos dentro del código, no es necesario interactuar con el juego de conversión de bases del servidor.

Se extrajeron los bytes crudos y se procesaron directamente mediante un intérprete local de Python aplicando la máscara de bits simétrica:

* Se define la cadena cifrada original en memoria.
* Se utiliza la contraseña fija `enkidu` para revertir la función XOR.
* Se imprime la bandera limpia sin interactuar con la lógica condicional del script del reto.

## Flag Obtenida:
picoCTF{4ll_y0ur_b4535_9c3b7d4d}