# Safe Opener 2

## Descripción del Reto
Este reto de nivel intermedio (100 puntos) pertenece a la categoría de Ingeniería Inversa (*Reverse Engineering*). Consiste en analizar un archivo `.class` de Java (código compilado en bytecode) para recuperar una contraseña o llave perdida que permita abrir una caja fuerte.

## Análisis Técnico (Information Disclosure via Hardcoded Plaintext)
En el desarrollo de software seguro, almacenar credenciales, llaves de cifrado o secretos directamente en el código fuente (*hardcoding*) es una vulnerabilidad crítica de divulgación de información. 

Aunque los archivos `.class` están compilados en bytecode binario ejecutable por la Máquina Virtual de Java (JVM), las constantes de tipo cadena de texto (*String Literals*) se almacenan intactas en texto plano dentro de una sección del archivo llamada el **Constant Pool** (Pool de Constantes). 

* **La Vulnerabilidad**: Un atacante no necesita descompilar ni ejecutar el programa de forma dinámica; basta con inspeccionar los strings binarios crudos del archivo para extraer la información sensible expuesta.

## Proceso de Reconstrucción
1. Se descargó el archivo binario compilado `SafeOpener.class`.
2. Al tratarse de un archivo de Java compilado, se realizó un análisis estático de cadenas de texto leyendo el archivo de forma directa.
3. Se identificó que dentro de la estructura de literales del binario se encontraba la bandera completa de picoCTF expuesta en texto legible:
   
   ```
   ,picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_de45efd6}