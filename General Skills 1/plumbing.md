# plumbing

## Descripción del Reto
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag? Connect to `fickle-tempest.picoctf.net 54706`.

## Solución
Al conectarnos al servidor mediante `netcat`, este nos devuelve una cantidad masiva de líneas de texto que hace imposible buscar la bandera manualmente. 
Para resolverlo, utilizamos el concepto de "tuberías" (pipes, `|`) en Linux. Esto nos permite tomar la salida estándar del comando `nc` y pasarla como entrada al comando `grep` para filtrar específicamente la cadena que necesitamos.

Comando utilizado:
`nc fickle-tempest.picoctf.net 54706 | grep "picoCTF"`

Al ejecutarlo, `grep` aísla y nos imprime únicamente la línea que contiene la bandera.

## Bandera
`picoCTF{digital_plumb3r_11fffFE5}`