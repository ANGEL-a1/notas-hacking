# fixme2

Descripción del Reto
Este reto nos presenta un script en Python (fixme2.py) que contiene un error de sintaxis en su bloque condicional que impide su ejecución. El objetivo es realizar un análisis estático sobre el código fuente para corregir el operador lógico erróneo, eludir la ejecución dañada y descifrar la cadena de texto protegida, la cual corresponde a la bandera (flag) del reto.

Análisis del Código Fuente
Al revisar el script, observamos que el programa implementa las siguientes mecánicas:

1. Define una cadena cifrada en memoria (`flag_enc`) mediante un arreglo de caracteres individuales.
2. Invoca la función `str_xor(flag_enc, 'enkidu')` para almacenar el resultado en la variable `flag`.
3. El desarrollador intentó validar que el resultado no estuviera vacío utilizando una sentencia `if flag = "":`. Al emplear un solo signo de igualdad (`=`), el intérprete de Python reconoce una operación de asignación en lugar de una comparación lógica, interrumpiendo el flujo con un `SyntaxError`.

Proceso de Reconstrucción (De-ofuscación y Corrección)
Para resolverlo, se aplicó ingeniería inversa básica corrigiendo el operador condicional del script original. Debido a que tanto el arreglo binario cifrado (`flag_enc`) como la clave simétrica (`enkidu`) se encuentran grabadas de manera estática en el archivo fuente, basta con parchar el condicional o ejecutar el algoritmo de forma directa en un script local:

* Se sustituye el operador de asignación (`=`) por el operador de comparación de igualdad (`==`).
* Se ejecuta el descifrado utilizando la contraseña estática `enkidu`.
* Se procesa la máscara de bits simétrica de la función XOR para extraer la bandera estructurada.

Flag Obtenida:
picoCTF{3qu4l1ty_n0t_4551gnm3nt_f6a5aefc}