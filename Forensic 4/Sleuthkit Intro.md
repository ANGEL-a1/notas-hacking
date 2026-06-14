# Sleuthkit Intro

## Descripción del Reto

Este reto de nivel medio (100 puntos) pertenece a la categoría de Forensics y tiene como objetivo familiarizar al participante con el uso de herramientas de análisis forense de discos, específicamente **The Sleuth Kit (TSK)**. Se proporciona una imagen de disco comprimida (`disk.img.gz`) y se solicita identificar el tamaño de la partición Linux contenida en la imagen. Posteriormente, el resultado debe enviarse a un servicio remoto que valida la respuesta y entrega la bandera.

## Análisis de la Imagen de Disco

Las imágenes de disco almacenan una copia exacta de la estructura de almacenamiento de un sistema, incluyendo la tabla de particiones, sistemas de archivos y datos.

Para examinar la distribución de particiones se utiliza la herramienta `mmls`, incluida en The Sleuth Kit. Esta herramienta permite visualizar la tabla de particiones y obtener información como:

- Sector de inicio de cada partición.

- Sector final.

- Tamaño total en sectores.

- Tipo de partición.


La ejecución del comando:

```bash
mmls disk.img
```

produce una salida similar a:

```text
DOS Partition Table
Offset Sector: 0

Slot      Start        End          Length       Description
00:000    0000000000   0000002047   0000002048   Primary Table (#0)
00:001    0000002048   0000204799   0000202752   Linux (0x83)
```

Del análisis se observa que la partición Linux posee un tamaño de:

```text
202752 sectores
```

## Validación con el Servicio Remoto

Una vez identificado el tamaño de la partición, se establece conexión con el servicio de validación proporcionado por el reto mediante Netcat:

```bash
nc saturn.picoctf.net 64451
```

El servicio solicita el tamaño de la partición Linux. Al ingresar:

```text
202752
```

el sistema verifica la respuesta y devuelve la bandera correspondiente.

## Herramientas Utilizadas

- **mmls** (The Sleuth Kit): análisis de tablas de particiones.

- **Netcat (nc)**: comunicación con el servicio remoto de validación.

- **Linux/WebShell**: entorno de ejecución para herramientas forenses.


## Flag Obtenida

`picoCTF{mm15_f7w!}`