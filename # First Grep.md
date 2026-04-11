# First Grep

## Descripción del Reto
Can you find the flag in the file? This would be really tedious to look through manually, something tells me there is a better way. The flag is in this file.

## Solución
Para resolver este reto, descargamos el archivo proporcionado, el cual contiene una gran cantidad de texto. En lugar de buscar manualmente, utilizamos el comando `grep` en la terminal de Linux (o la función de búsqueda `Ctrl + F` en un editor de texto en Windows) para buscar la cadena específica que caracteriza a las banderas del formato CTF. 

Al buscar la palabra clave "picoCTF" dentro del archivo, encontramos la bandera oculta.

## Bandera
`picoCTF{grep_is_good_to_find_things_01aE5e9d}`