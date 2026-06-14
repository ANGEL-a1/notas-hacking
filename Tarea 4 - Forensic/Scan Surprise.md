# Scan Surprise

## Descripción del Reto

Este reto de nivel fácil (50 puntos) pertenece a la categoría de **Forensics** y proporciona un archivo comprimido llamado `challenge.zip`.

La descripción menciona que la bandera ya no se encuentra como texto plano, sino que ha sido almacenada como una imagen.

Las pistas indican claramente la dirección de la solución:

- Los códigos QR pueden almacenar cualquier tipo de información.
- Los teléfonos modernos pueden escanear códigos QR de forma nativa.
- Herramientas como `zbar-tools` permiten decodificarlos desde la terminal.

---

## Análisis Inicial

Se comenzó inspeccionando el contenido del archivo ZIP:

```bash
unzip challenge.zip
```

La extracción reveló la siguiente estructura:

```text
home/
└── ctf-player/
    └── drop-in/
        └── flag.png
```

La presencia de una imagen llamada `flag.png` sugería inmediatamente que el contenido relevante se encontraba oculto visualmente.

---

## Inspección de la Imagen

Al abrir `flag.png` se observó que la imagen era un **código QR**.

Los códigos QR son matrices bidimensionales capaces de almacenar:

- URLs
- Texto plano
- Credenciales
- Datos binarios
- Banderas de CTF

---

## Decodificación del Código QR

Para recuperar el contenido se puede utilizar:

### Desde un teléfono móvil

Abrir la cámara y apuntar hacia el código QR.

### Desde Linux

Utilizando `zbarimg`:

```bash
zbarimg flag.png
```

Salida:

```text
QR-Code:picoCTF{p33k_@_b00_0194a007}
```

---

## Flag Obtenida

```text
picoCTF{p33k_@_b00_0194a007}
```