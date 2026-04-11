# Glitch Cat

## Descripción del Reto
Our flag printing service has started glitching!
Additional details will be available after launching your challenge instance.
Comando usado: `nc saturn.picoctf.net 50043`

## Solución
Al conectarnos al servidor proporcionado mediante la herramienta `netcat` (nc), el servidor nos devolvió una cadena de texto fragmentada y construida como código válido de Python:
`'picoCTF{gl17ch_m3_n07_' + chr(0x39) + chr(0x63) + chr(0x34) + chr(0x32) + chr(0x61) + chr(0x34) + chr(0x35) + chr(0x64) + '}'`

El servidor utilizó la función `chr()` para representar caracteres ASCII a partir de sus valores hexadecimales. Al evaluar esta expresión en un intérprete de Python, las funciones se traducen a sus respectivos caracteres (`9c42a45d`), revelando la bandera completa.

## Bandera
`picoCTF{gl17ch_m3_n07_9c42a45d}`