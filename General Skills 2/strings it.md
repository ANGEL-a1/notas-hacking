# strings it

## Descripción del Reto
Can you find the flag in this file without actually running it?

## Solución 
Para resolver este reto, se nos proporciona un archivo binario llamado `strings`. Al ser un archivo ejecutable, su contenido crudo es ilegible; sin embargo, podemos utilizar la herramienta `strings` para extraer las secuencias de caracteres imprimibles.

Para encontrar la bandera de forma eficiente sin revisar manualmente miles de líneas de texto, utilizamos un "pipe" para filtrar la salida directamente con `grep`:

`strings strings | grep "picoCTF"`

Al ejecutar este comando, el sistema procesa los datos del binario, filtra el ruido y revela la bandera directamente en la salida de la terminal.

## Bandera:
`picoCTF{5tRIng5_1T_FB7D7Bb6}`