# flag_shop

# Descripción del Reto

Este reto de nivel medio (300 puntos) pertenece a la categoría **General Skills** y se centra en la explotación de un **Integer Overflow** en un programa escrito en C.

El objetivo consiste en manipular el saldo de una cuenta virtual para adquirir una bandera cuyo costo excede ampliamente los fondos iniciales disponibles. Para lograrlo es necesario aprovechar el comportamiento de los enteros con signo de 32 bits y el sistema de **complemento a dos**, provocando un desbordamiento aritmético que incremente artificialmente el saldo del usuario.

---

## Análisis del Código Fuente

El reto proporciona el código fuente del programa:

```c
int account_balance = 1100;
```

Inicialmente el usuario dispone únicamente de:

```text
1100 dólares
```

La bandera real puede adquirirse únicamente si el saldo supera:

```c
if(account_balance > 100000)
```

Sin embargo, el usuario comienza muy por debajo de ese valor.

---

## Identificación de la Vulnerabilidad

Al revisar la opción de compra de banderas económicas se encuentra el siguiente fragmento:

```c
int total_cost = 0;
total_cost = 900 * number_flags;
```

La variable `total_cost` es de tipo `int`, lo que implica que utiliza 32 bits con signo.

Posteriormente el programa valida:

```c
if(total_cost <= account_balance)
{
    account_balance = account_balance - total_cost;
}
```

Si `total_cost` se convierte en un número negativo mediante un overflow, la resta terminará incrementando el saldo en lugar de disminuirlo.

---

## Comprendiendo el Overflow

Un entero con signo de 32 bits tiene como valor máximo:

```text
2147483647
```

Para provocar un desbordamiento:

```text
900 × number_flags > 2147483647
```

Despejando:

```text
number_flags > 2386092
```

Por lo tanto, cualquier valor superior a `2386092` producirá un overflow.

---

## Explotación

Se establece conexión con el servicio:

```bash
nc fickle-tempest.picoctf.net 59063
```

A continuación se selecciona la compra de banderas económicas:

```text
2
```

```text
1
```

Y se introduce una cantidad suficientemente grande:

```text
2386095
```

El programa realiza la multiplicación:

```text
900 × 2386095
```

El resultado excede el rango permitido para un entero con signo de 32 bits y se convierte en un valor negativo debido al comportamiento del complemento a dos.

Como consecuencia, la operación:

```c
account_balance = account_balance - total_cost;
```

equivale realmente a:

```text
saldo = saldo + valor_grande
```

incrementando el saldo por encima de los 100000 dólares requeridos.

---

## Compra de la Bandera

Una vez obtenido un saldo elevado, se vuelve al menú principal y se selecciona:

```text
2
```

```text
2
```

```text
1
```

Lo que corresponde a:

```text
Buy Flags
1337 Flag
Comprar 1 unidad
```

Ahora la condición:

```c
if(account_balance > 100000)
```

se cumple satisfactoriamente y el programa revela el contenido de `flag.txt`.

---

## Flag Obtenida

```text
picoCTF{m0n3y_bag5_39AF2bE1}
```
