## PW Crack 3
# Descripción del Reto
Este reto eleva la complejidad al implementar una rutina de autenticación basada en funciones de hash criptográfico (MD5) en lugar de comparaciones en texto plano. El objetivo es realizar un análisis estático del script (level3.py) para identificar un diccionario acotado de contraseñas candidatas, automatizar un ataque de fuerza bruta local comparando hashes y descifrar el archivo complementario (level3.flag.txt.enc) para reconstruir la bandera (flag) del reto.

Análisis del Código Fuente
Al revisar el script, observamos que el programa implementa las siguientes validaciones:

1. Solicita al usuario ingresar una contraseña y la procesa a través de la función `hash_pw()`, la cual convierte la cadena a bytes y calcula su digestión MD5 (`hashlib.md5()`).
2. Compara el hash resultante contra los bytes almacenados en el archivo externo `level3.hash.bin`.
3. El desarrollador incluyó un arreglo estático al final del archivo (`pos_pw_list`) que contiene únicamente 7 cadenas de texto como posibles contraseñas candidatas.

Proceso de Reconstrucción (Fuerza Bruta Local)
Para resolverlo, se diseñó un script de automatización que itera sobre el diccionario expuesto en el código fuente, calculando el hash MD5 local de cada elemento y comparándolo directamente con los bytes del archivo binario. Este bypass estático descarta la interacción manual:

* Se cargaron los bytes puros de `level3.hash.bin` y `level3.flag.txt.enc` en modo de lectura binaria para evitar alteraciones de codificación de Windows.
* Se identificó la colisión exacta del hash correspondiente a la contraseña correcta.
* Se inyectó la clave descubierta en el algoritmo XOR simétrico para extraer la bandera estructurada.

# Flag Obtenida:

picoCTF{m45h_fl1ng1ng_2b072a90}