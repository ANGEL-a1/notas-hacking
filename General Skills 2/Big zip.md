# Big zip

## Descripción del Reto
Unzip this archive and find the flag.

## Solución
Para resolver este reto, descargamos un archivo comprimido `.zip` que contiene múltiples directorios anidados y una gran cantidad de archivos de texto.
En lugar de buscar la bandera manualmente en cada archivo, utilizamos el comando `grep` con la bandera `-r` (recursivo) para buscar una cadena específica en todos los archivos del directorio actual y sus subdirectorios de manera automática.

Comandos utilizados:
`unzip big-zip-files.zip`
`grep -r "picoCTF" .`

El comando nos devuelve la ruta exacta del archivo y la línea que contiene la bandera oculta.

## Bandera
`picoCTF{gr3p_15_m4g1c_ef8790dc}`