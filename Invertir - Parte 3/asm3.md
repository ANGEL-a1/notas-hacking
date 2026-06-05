### Problem

¿Qué devuelve `asm3(0xb75a8f13, 0xe1860bd7, 0xc8e62f81)`? Envíe la bandera como un valor hexadecimal (comenzando con '0x'). NOTA: Su envío para esta pregunta NO estará en el formato de bandera normal.

### Solution

Analicemos el código fuente proporcionado:

Fragmento de código

```
asm3:
	<+0>:	endbr32 
	<+4>:	push   ebp
	<+5>:	mov    ebp,esp
	<+7>:	xor    eax,eax
	<+9>:	mov    ah,BYTE PTR [ebp+0x9]
	<+12>:	shl    ax,0x10
	<+16>:	sub    al,BYTE PTR [ebp+0xf]
	<+19>:	add    ah,BYTE PTR [ebp+0xd]
	<+22>:	xor    ax,WORD PTR [ebp+0x12]
	<+26>:	nop
	<+27>:	pop    ebp
	<+28>:	ret    
```

#### 1. Mapeo de la Pila (Stack)

La función recibe tres argumentos de 4 bytes (32 bits) cada uno: `asm3(0xb75a8f13, 0xe1860bd7, 0xc8e62f81)`.

Al estar en una arquitectura x86 de 32 bits (Little-Endian), los bytes se almacenan invertidos en la memoria. El mapa exacto de bytes en la pila respecto a `ebp` es el siguiente:

- **Argumento 1 (`0xb75a8f13`)** en `[ebp+0x8]`:

- `[ebp+0x8]` = `0x13`

- `[ebp+0x9]` = `0x8f`

- `[ebp+0xa]` = `0x5a`

- `[ebp+0xb]` = `0xb7`

- **Argumento 2 (`0xe1860bd7`)** en `[ebp+0xc]`:

- `[ebp+0xc]` = `0xd7`

- `[ebp+0xd]` = `0x0b`

- `[ebp+0xe]` = `0x86`

- `[ebp+0xf]` = `0xe1`

- **Argumento 3 (`0xc8e62f81`)** en `[ebp+0x10]`:

- `[ebp+0x10]` = `0x81`

- `[ebp+0x11]` = `0x2f`

- `[ebp+0x12]` = `0xe6`

- `[ebp+0x13]` = `0xc8`


#### 2. Ejecución Paso a Paso

- **`<+7>: xor eax,eax`**

Limpia el registro `eax`. Ahora `eax = 0x00000000`.

- **`<+9>: mov ah,BYTE PTR [ebp+0x9]`**

Mueve el byte en `[ebp+0x9]` (`0x8f`) a la parte alta de `ax` (`ah`).

- `eax = 0x00008f00`

- **`<+12>: shl ax,0x10`**

Desplaza `ax` (los 16 bits inferiores de `eax`) a la izquierda por `0x10` (16 veces). Como `ax` sólo tiene 16 bits de tamaño, desplazarlo 16 posiciones hace que todos sus bits salgan del registro, dejando `ax` completamente en cero.

- `eax = 0x00000000`

- **`<+16>: sub al,BYTE PTR [ebp+0xf]`**

Resta el byte en `[ebp+0xf]` (`0xe1`) a `al` (`0x00`).

- Operación: $0x00 - 0xe1 = 0x1f$ (por desbordamiento de 8 bits).

- `eax = 0x0000001f`

- **`<+19>: add ah,BYTE PTR [ebp+0xd]`**

Suma el byte en `[ebp+0xd]` (`0x0b`) a `ah` (`0x00`).

- Operación: $0x00 + 0x0b = 0x0b$.

- `eax = 0x00000b1f`

- **`<+22>: xor ax,WORD PTR [ebp+0x12]`**

Realiza una operación XOR entre `ax` (`0x0b1f`) y la palabra (2 bytes) que empieza en `[ebp+0x12]`.

- Leyendo 2 bytes desde `[ebp+0x12]` en Little-Endian: `[ebp+0x12]` es `0xe6` y `[ebp+0x13]` es `0xc8`, por lo que la palabra completa es `0xc8e6`.

- Operación: $0x0b1f \oplus 0xc8e6$


```
  0000 1011 0001 1111  (0x0b1f)
XOR
  1100 1000 1110 0110  (0xc8e6)
---------------------
  1100 0011 1111 1001  (0xc3f9)
```

- `ax` cambia a `0xc3f9`.

- `eax = 0x0000c3f9`

#### 3. Finalización

Las líneas finales limpian el marco de la pila y retornan el valor almacenado en `eax`.

### Flag

0xc3f9

