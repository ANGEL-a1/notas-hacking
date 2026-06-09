## Serpentine

## Descripción del Reto
Este reto nos presenta un script interactivo en Python (serpentine.py) que simula un menú de opciones por consola ("serpentine encourager"). El objetivo es realizar un análisis estático del flujo lógico del programa para identificar funciones huérfanas o desvinculadas de la interfaz de usuario, eludir las restricciones del menú y forzar la ejecución de la subrutina de descifrado para extraer la bandera (flag) del reto.

Análisis del Código Fuente
Al revisar el script, observamos que el programa implementa las siguientes mecánicas:

1. El flujo de control principal `main()` contiene un ciclo infinito `while True` que evalúa la entrada del usuario mediante condicionales `if-elif`.
2. Al seleccionar la opción de imprimir la bandera (`choice == 'b'`), el programa ejecuta un `print()` estático con un mensaje de error falso que afirma que la función fue extraviada.
3. En la sección superior del código, la función legítima `print_flag()` está completamente declarada e invoca al método `str_xor(flag_enc, 'enkidu')` utilizando una llave estática fija.

Proceso de Reconstrucción (Bypass de Flujo Lógico)
Para resolverlo, se aplicó ingeniería inversa sobre el flujo de ejecución reemplazando el punto de entrada interactivo por una invocación directa a la subrutina huérfana. Este bypass descarta el menú manipulado:

* Se identificó que las variables del cifrado XOR y la llave de descifrado `"enkidu"` se encontraban hardcoded en texto plano.
* Se aisló el algoritmo de de-ofuscación en un script local de ejecución autónoma.
* Se forzó la llamada directa a `print_flag()`, forzando el descifrado matemático de los bytes posicionales (`chr()`) para reconstruir la bandera estructurada.

## Flag Obtenida:

picoCTF{7h3_r04d_l355_7r4v3l3d_8e47d128}