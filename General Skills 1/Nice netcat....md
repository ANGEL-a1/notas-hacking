# Nice netcat...

## Descripción del Reto
There is a nice program that you can talk to by using this command in a shell:
`$ nc wily-courier.picoctf.net 56315`, but it doesn't speak English...

## Solución
Al conectarnos al servidor mediante `netcat`, el programa nos devuelve una lista de números en lugar de texto. La pista de "no habla inglés" nos indica que estos números representan caracteres codificados.

Cada número de la salida es el valor decimal en la tabla ASCII de un caracter. Para automatizar la decodificación directamente en la terminal sin hacerlo manualmente, concatenamos la salida con el comando `awk` para formatear los números de vuelta a caracteres:

`nc wily-courier.picoctf.net 56315 | awk '{printf "%c", $1}'`

Al ejecutarlo, la terminal nos imprime la bandera decodificada.

## Bandera
`picoCTF{g00d_k1tty!_n1c3_k1tty!_d9476}`