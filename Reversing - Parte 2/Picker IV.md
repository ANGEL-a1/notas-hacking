# Picker IV

## Descripción del Reto
Este reto de nivel intermedio (100 puntos) pertenece a la categoría de Explotación de Binarios (*Binary Exploitation*) y concluye la serie de retos *Picker*. A diferencia de sus predecesores basados en scripts interpretados de Python, este entorno expone un binario real compilado nativamente en lenguaje C (arquitectura x86_64). El objetivo consiste en identificar la dirección de memoria estática de una función restringida e ingresarla directamente para desviar el puntero de instrucciones del procesador.

## Análisis Técnico (Arbitrary Function Pointer Execution)
Al analizar el flujo del archivo fuente `picker-IV.c`, la función `main` implementa una entrada numérica directa formateada en hexadecimal mediante `scanf` y la almacena en una variable de tipo entero:

```c
unsigned int val;
printf("Enter the address in hex to jump to, excluding '0x': ");
scanf("%x", &val);

void (*foo)(void) = (void (*)())val;
foo();
````

- **La Vulnerabilidad**: El binario toma el valor proveído por el usuario (`val`), realiza un moldeo de tipo (_type casting_) explícito para convertirlo en un puntero a función (`void (*foo)(void)`) y lo invoca de forma directa (`foo()`). No existe validación, límites de rango, ni listas de control de acceso sobre las direcciones a las que el hilo de ejecución puede saltar.

- **La Solución**: Dado que el binario no cuenta con mecanismos de aleatorización en la carga de memoria dinámicos (como ASLR total o PIE ejecutable habilitado en el segmento del reto), las funciones se posicionan en direcciones estáticas fijos. Inspeccionando la tabla de símbolos del binario (`.symtab`), es posible extraer el desplazamiento hexadecimal exacto de la subrutina restringida `win()`.


## Proceso de Reconstrucción

1. Se auditó la estructura de símbolos del ejecutable `picker-IV` buscando la entrada correspondiente a la rutina encargada de leer los secretos del sistema.

2. Se localizó el identificador de la función `win`, cuyo registro en la tabla reflejó el siguiente desplazamiento de memoria estático:


    ```
   Dirección de salto extraída: 40129d
    ```

3. Se inició la sesión de explotación por red mediante sockets conectándose a la instancia asignada:

  ```
  nc saturn.picoctf.net 64886
  ```

4. Al recibir el prompt que solicita la dirección de salto, se ingresó el valor hexadecimal previamente identificado (excluyendo el prefijo de notación `0x`):

    ```
    40129d
    ```

5. El procesador desvió su flujo de ejecución ordinario saltando directamente a `win()`, validando la victoria e imprimiendo la bandera del servidor en texto plano.

## Flag Obtenida:

picoCTF{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_14bc5444}