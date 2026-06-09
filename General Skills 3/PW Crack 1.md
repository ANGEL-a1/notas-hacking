# PW Crack 1

Descripción del Reto
Este reto nos presenta un script de validación de contraseñas implementado en Python (level1.py) que protege una bandera cifrada localmente. El objetivo es realizar un análisis estático sobre el código fuente para identificar las credenciales hardcoded, eludir la entrada interactiva por consola y descifrar el archivo complementario (level1.flag.txt.enc) para reconstruir la bandera (flag) del reto.

Análisis del Código Fuente
Al revisar el script, observamos que el programa implementa las siguientes validaciones:

1. Solicita al usuario ingresar una contraseña a través de la consola mediante `input()`.
2. Utiliza una sentencia condicional `if (user_pw == "8713"):` para comprobar que la cadena coincida exactamente con el valor esperado.
3. Si la condición se cumple, lee los bytes del archivo cifrado `level1.flag.txt.enc` y ejecuta el método `str_xor(flag_enc.decode(), user_pw)` utilizando la misma contraseña como clave simétrica de descifrado.

Proceso de Reconstrucción (Bypass Estático)
Para resolverlo, se aplicó ingeniería inversa básica aislando las credenciales estáticas expuestas por el desarrollador. Debido a que la contraseña se encuentra en texto plano dentro del código, no es necesario interactuar con el prompt interactivo del servidor:

* Se identificó la clave de acceso estática `"8713"`.
* Se extrajeron los bytes crudos del archivo cifrado externo en modo de lectura binaria para evitar la corrupción de caracteres del sistema operativo local.
* Se ejecutó el algoritmo XOR en un script local de forma autónoma utilizando la llave descubierta para extraer la bandera estructurada.

Flag Obtenida:
picoCTF{545h_r1ng1ng_1b2fd683}