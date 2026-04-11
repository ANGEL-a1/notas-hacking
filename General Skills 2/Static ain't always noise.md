# Static ain't always noise

## Descripción del Reto
Can you look at the data in this binary? The bash script might help!

## Solución
Para resolver este reto, nos proporcionan un archivo binario compilado (`static`) y un script de bash (`ltdis.sh`). El script automatiza el uso de comandos de análisis estático como `objdump` para desensamblar la sección `.text` y `strings` para extraer las cadenas de caracteres legibles del binario.

Para resolverlo desde la terminal, ejecutamos el script pasándole el binario como argumento:
`./ltdis.sh static`

Esto genera un archivo llamado `static.ltdis.strings.txt`. Finalmente, utilizamos `grep` para aislar la bandera dentro de los resultados:
`grep "picoCTF" static.ltdis.strings.txt`

[cite_start]Al revisar los datos crudos del binario, el texto plano revela la bandera directamente.

## Bandera
[cite_start]`picoCTF{d15a5m_t34s3r_20335e41}`