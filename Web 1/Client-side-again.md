# Client-side-again

## Descripción del Reto
Este reto de nivel intermedio (200 puntos) pertenece a la categoría de Explotación Web y expande los conceptos de validación en el entorno del cliente implementando técnicas de ofuscación de código JavaScript. El objetivo es realizar ingeniería inversa sobre un script ofuscado para extraer y reordenar los fragmentos de la bandera almacenados en un arreglo del navegador.

## Análisis Técnico (Ingeniería Inversa de Código Ofuscado)
Delegar procesos de autenticación críticos al lado del cliente sigue siendo un fallo de diseño arquitectónico grave. Aunque el código sea transformado mediante un ofuscador para dificultar su lectura estática (renombrando variables, aplicando transformaciones matemáticas e indexando cadenas en arreglos dinámicos), el navegador requiere la ejecución del script puro en memoria.

* **Estructura de Ocultamiento**: El script utiliza un arreglo de almacenamiento de strings global (`_0x5a46`) que contiene sub-cadenas como `'picoCTF{'`, `'not_this'`, `'_again_4'` y `'daf93}'`. Este arreglo es rotado cíclicamente en memoria mediante una función de desplazamiento antes de evaluar las porciones de la entrada del usuario usando `.substring()`.

## Proceso de Reconstrucción
1. Se inspeccionaron las fuentes del sitio mediante la pestaña *Sources* de las DevTools en Opera GX.
2. Se identificó el bloque de código JavaScript ofuscado y el arreglo de strings base.
3. Se analizó el flujo de las sentencias condicionales e índices de texto, determinando el orden de concatenación de los elementos de control de identidad de la función `verify()`.
4. Se reconstruyeron secuencialmente los fragmentos conforme a la sintaxis del formato de picoCTF.

## Flag Obtenida:
picoCTF{not_this_again_4daf93}