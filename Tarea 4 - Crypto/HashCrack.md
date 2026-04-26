## Descripción
El reto consiste en conectarse a un servidor remoto mediante `netcat` que nos proporciona una serie de hashes. Debemos identificar el tipo de hash y proporcionar la contraseña en texto plano correspondiente para avanzar hasta obtener la flag.

## Solución
Se utilizó el comando:
`nc verbal-sleep.picoctf.net 56487`

Se resolvieron los siguientes hashes:
1. **MD5**: `482c811da5d5b4bc6d497ffa98491e38` -> Password: `password123`
2. **SHA-1**: `b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3` -> Password: `letmein`
3. **SHA-256**: `916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745` -> Password: `qwerty098`

## Flag
`picoCTF{UseStr0nG_h@shEs_&PaSswDs!_eb2f8459}`