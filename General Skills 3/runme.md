## runme

# Descripción del Reto
Este reto nos presenta un script básico en Python (runme.py) cuyo único propósito es imprimir una cadena de texto en la consola. El objetivo es realizar un análisis estático directo sobre el código fuente para extraer la bandera (flag) del reto sin necesidad de interactuar con entornos de ejecución adicionales.

Análisis del Código Fuente
Al revisar el script, observamos que el programa implementa las siguientes mecánicas:

1. Declara una variable de tipo cadena llamada `flag` que almacena el token de la competencia en texto plano (hardcoded).
2. Invoca la función nativa `print(flag)` para desplegar el contenido directamente en la salida estándar de la terminal.
3. El archivo no cuenta con lógica condicional, ofuscación de variables ni rutinas de cifrado simétrico.

Proceso de Reconstrucción (Análisis Estático)
Para resolverlo, se aplicó un análisis estático inmediato sobre el archivo descargado. Dado que el desarrollador dejó la credencial expuesta en texto claro dentro del flujo principal del programa, no es necesario ejecutar el script ni realizar ingeniería inversa compleja:

* Se abrió el archivo fuente en el editor de texto.
* Se localizó la asignación directa de la variable principal.
* Se extrajo la bandera estructurada de forma inmediata.

# Flag Obtenida:
picoCTF{run_s4n1ty_run}