### Descripción del Reto

El mecanismo de validación de este reto (`VaultDoor4.java`) se basa en comparar los bytes de la contraseña ingresada con un arreglo estático de control llamado `myBytes`. La ofuscación consiste en que el desarrollador dividió los 32 bytes del arreglo en **cuatro formatos y bases numéricas diferentes**: números decimales, valores hexadecimales, números octales y caracteres en texto plano.

### Análisis de las Bases Numéricas y Traducción ASCII

Para resolver el reto, se mapea cada elemento del arreglo de bytes a su equivalente de carácter utilizando la tabla estándar ASCII:

#### 1. Bloque 1: Decimales (Base 10)

Representación numérica estándar. Los enteros corresponden directamente al índice ASCII.

- `106` $\rightarrow$ `'j'`
- `85` $\rightarrow$ `'U'`
- `53` $\rightarrow$ `'5'`
- `116` $\rightarrow$ `'t'`
- `95` $\rightarrow$ `'_'`
- `52` $\rightarrow$ `'4'`
- `95` $\rightarrow$ `'_'`
- `98` $\rightarrow$ `'b'`

#### 2. Bloque 2: Hexadecimales (Base 16)

Identificados en código por el prefijo `0x`.

- `0x55` $\rightarrow$ `'U'`
- `0x6e` $\rightarrow$ `'n'`
- `0x43` $\rightarrow$ `'C'`
- `0x68` $\rightarrow$ `'h'`
- `0x5f` $\rightarrow$ `'_'`
- `0x30` $\rightarrow$ `'0'`
- `0x66` $\rightarrow$ `'f'`
- `0x5f` $\rightarrow$ `'_'`

#### 3. Bloque 3: Octales (Base 8)

**Nota de Ingeniería Inversa:** En lenguajes derivados de C (como Java), cualquier número entero que comience con un cero (`0`) sin ninguna letra posterior se interpreta automáticamente como una constante en **base 8**.

- `0142` $\rightarrow$ $1 \times 8^2 + 4 \times 8^1 + 2 \times 8^0 = 98$ (Decimal) $\rightarrow$ `'b'`
- `0131` $\rightarrow$ $1 \times 8^2 + 3 \times 8^1 + 1 \times 8^0 = 89$ (Decimal) $\rightarrow$ `'Y'`
- `0164` $\rightarrow$ $1 \times 8^2 + 6 \times 8^1 + 4 \times 8^0 = 116$ (Decimal) $\rightarrow$ `'t'`
- `063` $\rightarrow$ $6 \times 8^1 + 3 \times 8^0 = 51$ (Decimal) $\rightarrow$ `'3'`
- `0163` $\rightarrow$ $1 \times 8^2 + 6 \times 8^1 + 3 \times 8^0 = 115$ (Decimal) $\rightarrow$ `'s'`
- `0137` $\rightarrow$ $1 \times 8^2 + 3 \times 8^1 + 7 \times 8^0 = 95$ (Decimal) $\rightarrow$ `'_'`
- `066` $\rightarrow$ $6 \times 8^1 + 6 \times 8^0 = 54$ (Decimal) $\rightarrow$ `'6'`
- `064` $\rightarrow$ $6 \times 8^1 + 4 \times 8^0 = 52$ (Decimal) $\rightarrow$ `'4'`

#### 4. Bloque 4: Caracteres planos (ASCII directo)

Al estar declarados explícitamente entre comillas simples (`' '`), el compilador ya los almacena con su valor numérico de byte crudo:

- `'e'`, `'1'`, `'3'`, `'d'`, `'0'`, `'0'`, `'b'`, `'2'`

###### **Flag Obtenida:** `picoCTF{jU5t_4_bUnCh_0f_bYt3s_64e13d00b2}`