# Wave a flag

## Descripción del Reto
Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information... if you can find it!

## Solución
Para resolver este reto, se nos proporciona un archivo binario llamado `warm`. Al intentar ejecutarlo directamente, el programa nos indica que debemos pasarle un argumento para obtener ayuda.

Primero, otorgamos permisos de ejecución al archivo: `chmod +x warm`

Luego, lo ejecutamos utilizando el flag `-h` (help) como se nos sugiere en el mensaje inicial: `./warm -h`

Al solicitar la ayuda, el binario revela el mensaje oculto y muestra directamente la bandera en la terminal.

## Bandera:
`picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}`