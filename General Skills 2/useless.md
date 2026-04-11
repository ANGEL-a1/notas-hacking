# useless

## Descripción del Reto
There's an interesting script in the user's home directory. The work computer is running SSH. We've been given a script which performs some basic calculations, explore the script and find a flag.

## Solución
Para resolver este desafío, utilicé una conexión remota SSH al servidor proporcionado. Al explorar el entorno, localicé el script `useless`. Siguiendo las convenciones de sistemas Linux, consulté el manual de usuario (`man page`) del script para entender su funcionamiento.

Comandos utilizados:
1. Conexión SSH: `ssh -p 61752 picoplayer@saturn.picoctf.net`
2. Lectura del manual: `man useless | cat`

La bandera se encontraba oculta en la sección final de la documentación del manual.

## Bandera
`picoCTF{us3l3ss_ch4ll3ng3_3xpl0it3d_6140}`