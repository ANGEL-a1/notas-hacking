# First Find

## Descripción del Reto
Unzip this archive and find the file named 'uber-secret.txt'.

## Solución
Para resolver este reto, primero descargamos y descomprimimos el archivo proporcionado (`files.zip`). 
En lugar de buscar manualmente carpeta por carpeta, utilizamos el comando `find` en la terminal para localizar la ruta exacta del archivo objetivo.

Comandos teóricos utilizados:
`unzip files.zip`
`find . -name "uber-secret.txt"`

Una vez que obtenemos la ruta del archivo, usamos el comando `cat` para leer su contenido y visualizar la bandera.

## Bandera
`picoCTF{f1nd_15_f457_ab443fd1}`