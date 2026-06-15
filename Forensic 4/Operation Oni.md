# Operation Oni

## Descripción

Se proporciona una imagen de disco comprimida (`disk.img.gz`) y el objetivo es encontrar una clave SSH oculta para acceder a una máquina remota y obtener la flag.

## Información inicial

Archivo:

```bash
disk.img.gz
```

Acceso remoto:

```bash
ssh -i key_file -p <PORT> ctf-player@saturn.picoctf.net
```

---

## 1. Descompresión de la imagen

Al intentar descomprimir en el directorio personal apareció:

```bash
gzip -d disk.img.gz

gzip: disk.img: No space left on device
```

La razón era que `/home` tenía una cuota limitada (~128 MB).

Verificación:

```bash
df -h
```

Se copió la imagen a `/tmp` y se descomprimió allí:

```bash
cp disk.img.gz /tmp/
cd /tmp
gzip -d disk.img.gz
```

---

## 2. Identificación de particiones

Se utilizó `mmls` para identificar las particiones del disco:

```bash
mmls disk.img
```

Resultado:

```text
DOS Partition Table

Slot      Start      End        Length      Description

000:000   2048       206847     204800      Linux
000:001   206848     471039     264192      Linux
```

La partición interesante fue la segunda:

```text
Offset = 206848
```

---

## 3. Enumeración del sistema de archivos

Listado de la raíz:

```bash
fls -o 206848 disk.img
```

Se observó un directorio `/root`:

```text
470: root
```

Exploración:

```bash
fls -o 206848 disk.img 470
```

Resultado:

```text
r/r 2344: .ash_history
d/d 3916: .ssh
```

Contenido de `.ssh`:

```bash
fls -o 206848 disk.img 3916
```

Resultado:

```text
r/r 2345: id_ed25519
r/r 2346: id_ed25519.pub
```

---

## 4. Extracción de la clave privada

Se extrajo la clave privada con `icat`:

```bash
icat -o 206848 disk.img 2345 > id_ed25519
chmod 600 id_ed25519
```

Verificación:

```bash
head id_ed25519
```

Salida:

```text
-----BEGIN OPENSSH PRIVATE KEY-----
...
```

---

## 5. Acceso SSH

Con la clave privada recuperada:

```bash
ssh -i id_ed25519 -p <PORT> ctf-player@saturn.picoctf.net
```

Una vez autenticado se obtuvo acceso a la máquina objetivo.

---

## 6. Obtención de la flag

Dentro de la máquina:

```bash
find / -name flag.txt 2>/dev/null
cat flag.txt
```

## Flag

```text
picoCTF{k3y_5l3u7h_af277f77}
```