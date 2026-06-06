### Descripción del Reto

El mecanismo de seguridad de esta bóveda (`VaultDoor5.java`) eleva el nivel de ofuscación al combinar dos técnicas de codificación muy comunes en el desarrollo web: **URL Encoding** y **Base64**. El programa toma la contraseña ingresada, la procesa a través de ambos métodos y compara el resultado con una cadena estática final llamada `expected`.

### Análisis del Algoritmo de Ofuscación

Al revisar el código fuente, el método `checkPassword(String password)` realiza las siguientes transformaciones en cadena:

1. **`urlEncode(byte[] input)`**: A diferencia del comportamiento web estándar (que solo altera caracteres especiales), esta función personalizada fuerza a que **absolutamente todos** los caracteres de la contraseña se conviertan a su representación hexadecimal de dos dígitos, precedidos por un signo de porcentaje (`%`).

Java
    ```
    buf.append(String.format("%%%2x", input[i]));
    ```
2. **`base64Encode(byte[] input)`**: Toma la cadena de texto llena de porcentajes y la convierte a formato Base64 estándar.


Al final, el resultado se compara con la variable `expected`:

Plaintext

```
JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVmJTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2JTM0JTVmJTY1JTY0JTMwJTYyJTM0JTMyJTM4JTM4
```

### Proceso de Ingeniería Inversa (Paso a Paso)

Para revelar la contraseña original, debemos revertir el proceso de forma estricta, yendo de afuera hacia adentro:

#### Paso 1: Decodificación Base64

Al aplicar un decodificador Base64 a la cadena `expected`, obtenemos la cadena cruda de bytes en formato URL hexadecimal:

Plaintext

```
%63%30%6e%76%33%72%74%31%6e%67%5f%66%72%30%6d%5f%62%61%35%65%5f%36%34%5f%65%31%33%64%30%30%62%32
```

#### Paso 2: Decodificación URL / Hexadecimal a ASCII

Removemos los símbolos `%` y agrupamos los valores de dos en dos dígitos para traducirlos a caracteres legibles mediante la tabla ASCII:

- `%63` $\rightarrow$ **c**
- `%30` $\rightarrow$ **0**
- `%6e` $\rightarrow$ **n**
- `%76` $\rightarrow$ **v**
- `%33` $\rightarrow$ **3**
- `%72` $\rightarrow$ **r**
- `%74` $\rightarrow$ **t**
- `%31` $\rightarrow$ **1**
- `%6e` $\rightarrow$ **n**
- `%67` $\rightarrow$ **g**
- `%5f` $\rightarrow$ **_**
- `%66` $\rightarrow$ **f**
- `%72` $\rightarrow$ **r**
- `%30` $\rightarrow$ **0**
- `%6d` $\rightarrow$ **m**
- `%5f` $\rightarrow$ **_**
- `%62` $\rightarrow$ **b**
- `%61` $\rightarrow$ **a**
- `%35` $\rightarrow$ **5**
- `%65` $\rightarrow$ **e**
- `%5f` $\rightarrow$ **_**
- `%36` $\rightarrow$ **6**
- `%34` $\rightarrow$ **4**
- `%5f` $\rightarrow$ **_**
- `%65` $\rightarrow$ **e**
- `%31` $\rightarrow$ **1**
- `%33` $\rightarrow$ **3**
- `%64` $\rightarrow$ **d**
- `%30` $\rightarrow$ **0**
- `%30` $\rightarrow$ **0**
- `%62` $\rightarrow$ **b**
- `%32` $\rightarrow$ **2**

**Flag Obtenida:** `picoCTF{c0nv3rt1ng_fr0m_ba5e_64_e13d00b2}`