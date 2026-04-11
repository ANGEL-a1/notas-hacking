# what's a net cat?

## Descripción del Reto
Using netcat (nc) is going to be pretty important. Can you connect to `fickle-tempest.picoctf.net` at port `56434` to get the flag?

## Solución
Para resolver este reto, utilizamos la herramienta `netcat` (abreviada como `nc`) desde la terminal (Web Shell) para conectarnos al servidor y puerto especificados en la descripción. 
    
Comando utilizado:
`nc fickle-tempest.picoctf.net 56434`

Al establecer la conexión, el servidor nos devuelve automáticamente la bandera en texto claro junto con un mensaje de bienvenida.

## Bandera
`picoCTF{nEtCat_Mast3ry_5c7cC1a9}`