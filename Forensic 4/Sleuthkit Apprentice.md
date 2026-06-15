# Sleuthkit Apprentice

## Descripción

Se proporciona una imagen de disco comprimida (`disk.flag.img.gz`) y el objetivo es recuperar la flag utilizando herramientas de The Sleuth Kit.

## Objetivo

Analizar la imagen de disco, localizar el sistema de archivos correcto y recuperar la flag.

---

# 1. Descarga de la imagen

Se descargó la imagen desde el servidor de picoCTF:

```bash
wget https://artifacts.picoctf.net/c/138/disk.flag.img.gz
```

Verificación:

```bash
ls -lh disk.flag.img.gz
```

Tamaño aproximado:

```text
45 MB
```

---

# 2. Descompresión

Debido a las limitaciones de espacio en el directorio personal del webshell, se trabajó en `/tmp`.

```bash
cd /tmp
gzip -d disk.flag.img.gz
```

Resultado:

```text
disk.flag.img
```

---

# 3. Identificación de particiones

Se utilizó `mmls` para enumerar las particiones presentes en la imagen.

```bash
mmls disk.flag.img
```

Resultado:

```text
DOS Partition Table

Slot      Start      End        Length      Description

000:000   2048       206847     Linux (0x83)
000:001   206848     360447     Linux Swap / Solaris x86 (0x82)
000:002   360448     614399     Linux (0x83)
```

La partición más interesante fue la tercera:

```text
Offset = 360448
```

---

# 4. Exploración del sistema de archivos

Listar el contenido de la partición:

```bash
fls -o 360448 disk.flag.img
```

Resultado:

```text
home
boot
etc
proc
dev
tmp
lib
var
usr
bin
sbin
media
mnt
opt
root
run
srv
sys
swap
```

Se observó el directorio:

```text
root
```

---

# 5. Enumeración del directorio root

Exploración:

```bash
fls -o 360448 disk.flag.img 1995
```

Resultado:

```text
.ash_history
my_folder
```

El directorio sospechoso era:

```text
my_folder
```

---

# 6. Enumeración de my_folder

```bash
fls -o 360448 disk.flag.img 3981
```

Resultado:

```text
flag.txt
flag.uni.txt
```

Salida obtenida:

```text
r/r * 2082(realloc): flag.txt
r/r 2371: flag.uni.txt
```

Se observa que:

- `flag.txt` aparece como archivo eliminado (`realloc`).
    
- `flag.uni.txt` sigue accesible.
    

---

# 7. Recuperación de la flag

Extracción del archivo activo:

```bash
icat -o 360448 disk.flag.img 2371
```

# Flag

```text
picoCTF{by73_5urf3r_2f22df38}
```
