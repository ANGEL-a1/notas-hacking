### Problem

¿Qué devuelve `asm2(0x6, 0x21)`? Envíe la bandera como un valor hexadecimal (comenzando con '0x'). NOTA: Su envío para esta pregunta NO estará en el formato de bandera normal.

### Solution

Analicemos el código fuente proporcionado:

Fragmento de código

```
asm2:
	<+0>:	endbr32 
	<+4>:	push   ebp
	<+5>:	mov    ebp,esp
	<+7>:	sub    esp,0x10
	<+10>:	mov    eax,DWORD PTR [ebp+0xc]
	<+13>:	mov    DWORD PTR [ebp-0x4],eax
	<+16>:	mov    eax,DWORD PTR [ebp+0x8]
	<+19>:	mov    DWORD PTR [ebp-0x8],eax
	<+22>:	jmp    0x11d0 <asm2+35>
	<+24>:	add    DWORD PTR [ebp-0x4],0x1
	<+28>:	add    DWORD PTR [ebp-0x8],0x9f
	<+35>:	cmp    DWORD PTR [ebp-0x8],0x2d12
	<+42>:	jle    0x11c5 <asm2+24>
	<+44>:	mov    eax,DWORD PTR [ebp-0x4]
	<+47>:	leave  
	<+48>:	ret    
```

#### Inicialización de Variables

Llamamos a la función pasándole dos argumentos: `asm2(0x6, 0x21)`.

- El primer argumento `0x6` se ubica en la pila en `[ebp+0x8]`.

- El segundo argumento `0x21` se ubica en la pila en `[ebp+0xc]`.


En la línea `<+7>`, se reservan `0x10` bytes de espacio en la pila para variables locales. Luego se asignan los valores:

- En `<+10>` y `<+13>`: El segundo argumento (`0x21`) se mueve a la variable local `[ebp-0x4]`.

- En `<+16>` y `<+19>`: El primer argumento (`0x6`) se mueve a la variable local `[ebp-0x8]`.


Posteriormente, en la línea `<+22>`, se ejecuta un salto incondicional (`jmp`) hacia la condición del bucle en la línea `<+35>`.

#### Estructura del Bucle (Loop)

El bucle se evalúa abajo (`<+35>`) y salta hacia arriba (`<+24>`) si se cumple la condición:

Fragmento de código

```
	<+35>:	cmp    DWORD PTR [ebp-0x8],0x2d12
	<+42>:	jle    0x11c5 <asm2+24>
```

La instrucción `jle` significa _"jump if less or equal"_ (saltar si es menor o igual). El bucle continuará ejecutándose mientras el valor en `[ebp-0x8]` sea **menor o igual** a `0x2d12`.

Cada iteración del bucle modifica las variables locales en las líneas `<+24>` y `<+28>`:

- `[ebp-0x4] = [ebp-0x4] + 0x1` (incrementa en 1)

- `[ebp-0x8] = [ebp-0x8] + 0x9f` (incrementa en 0x9f)


#### Cálculo Matemático

Para evitar simular paso a paso cada vuelta, podemos calcular cuántas veces se ejecutará el bucle con una ecuación.

Queremos saber cuántas veces hay que sumar `0x9f` a nuestro valor inicial (`0x6`) para superar el límite estricto de `0x2d12`.

1. Convertimos los valores a decimal para facilitar la operación:

- Valor inicial `[ebp-0x8]` = $0x6 = 6$
- Incremento constante = $0x9f = 159$
- Límite de la condición = $0x2d12 = 11538$

2. Planteamos la desigualdad para romper el ciclo ($> 11538$):

$$6 + 159 \times \text{vueltas} > 11538$$

$$159 \times \text{vueltas} > 11532$$

$$\text{vueltas} > \frac{11532}{159} \approx 72.528$$


Dado que el salto ocurre cuando es _menor o igual_, la condición fallará (y el bucle terminará) exactamente en la vuelta **73**.

3. Ahora calculamos el valor final de la otra variable local `[ebp-0x4]`, la cual empezó en `0x21` y aumentó en `0x1` en cada una de las 73 iteraciones:

- Valor inicial en decimal: $0x21 = 33$
  
- Valor final = $33 + (1 \times 73) = 106$

4. Convertimos el resultado final `106` de regreso a hexadecimal:

- $106 = 0x6a$

#### Finalización

Fragmento de código

```
	<+44>:	mov    eax,DWORD PTR [ebp-0x4]
	<+47>:	leave  
	<+48>:	ret    
```

Al terminar el ciclo, el valor resultante en `[ebp-0x4]` (`0x6a`) se mueve al registro `eax` para ser devuelto como el retorno oficial de la función.

### Flag

0x6a