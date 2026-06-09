## Binhexa

# Descripción del Reto
Este reto evalúa la capacidad de realizar operaciones aritméticas y lógicas fundamentales directamente sobre el sistema de numeración binario (Base 2). El objetivo es interactuar con un servicio remoto vía Netcat, resolver una serie de problemas lógicos y de desplazamiento de bits de forma secuencial, y realizar una conversión final al sistema hexadecimal (Base 16) para desbloquear y extraer la bandera (flag) del reto.

Análisis del Código Fuente / Infraestructura
El reto no proporciona un archivo ejecutable local, sino un socket TCP expuesto mediante el comando `nc titan.picoctf.net 51149`. El servidor implementa un evaluador interactivo que valida operaciones en tiempo real, tales como:
1. Operaciones aritméticas elementales: Suma (`+`) y Multiplicación (`*`).
2. Operaciones lógicas a nivel de bits (Bitwise): `AND` (`&`) y `OR` (`|`).
3. Operadores de desplazamiento: Shift Left (`<<`) y Shift Right (`>>`).

Proceso de Reconstrucción (Evaluación y Conversión de Base)
Para resolverlo, se estableció la conexión remota y se automatizó/calculó el resultado de las operaciones binarias utilizando la shell interactiva de Python como entorno de validación para mitigar errores de acarreo manual:

* Se representaron los valores binarios en Python utilizando el prefijo `0b`.
* Se evaluaron las expresiones lógicas bitwise correspondientes según las solicitudes del servidor.
* Se aplicó el método nativo `hex()` sobre el acumulador final del juego para parsear el resultado binario remanente a su representación equivalente en texto hexadecimal plano, satisfaciendo la condición de salida de la rutina para imprimir la bandera.

# Flag Obtenida:

picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_d6f8047e}