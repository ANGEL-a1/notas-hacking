# PW Crack 2

## Descripción del Reto
Este reto nos presenta un script de validación de contraseñas implementado en Python (level2.py) que protege una bandera cifrada localmente. El objetivo es realizar un análisis estático sobre el código fuente para decodificar las credenciales ofuscadas en formato hexadecimal, eludir la entrada interactiva por consola y descifrar el archivo complementario (level2.flag.txt.enc) para reconstruir la bandera (flag) del reto.

Análisis del Código Fuente
Al revisar el script, observamos que el programa implementa las siguientes validaciones:

1. Solicita al usuario ingresar una contraseña a través de la consola mediante `input()`.
2. Utiliza una sentencia condicional `if( user_pw == chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65) ):` para comprobar la validez de la clave. El desarrollador intentó ocultar la credencial convirtiendo los valores posicionales a su representación entera ASCII mediante la función `chr()`.
3. Si la condición se cumple, lee los bytes del archivo cifrado `level2.flag.txt.enc` y ejecuta el método `str_xor(flag_enc.decode(), user_pw)` para realizar el descifrado simétrico.

Proceso de Reconstrucción (De-ofuscación y Bypass)
Para resolverlo, se aplicó ingeniería inversa básica traduciendo los bytes hardcoded del condicional a texto plano, lo que reveló la contraseña estática `"39ce"`. Debido a que la clave es fija, no es necesario interactuar con el prompt interactivo del servidor:

* Se reconstruyó la contraseña traduciendo los valores hexadecimales (`0x33`=3, `0x39`=9, `0x63`=c, `0x65`=e).
* Se extrajeron los bytes crudos del archivo cifrado externo en modo de lectura binaria para prevenir la corrupción de caracteres especiales y pérdida de bytes de control por parte del sistema operativo local.
* Se ejecutó el algoritmo XOR de forma autónoma usando la llave descubierta para extraer la bandera estructurada.

# Flag Obtenida:
picoCTF{tr45h_51ng1ng_502ec42e}