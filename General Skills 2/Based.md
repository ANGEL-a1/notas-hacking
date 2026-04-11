# Based

## Descripción del Reto
Para ser un verdadero "1337", se deben entender diferentes codificaciones de datos. Este reto pone a prueba la velocidad para convertir valores de distintas bases a texto ASCII antes de que expire el tiempo (45 segundos por ronda).

## Solución
El reto se resolvió mediante una conexión interactiva vía Netcat. Se realizaron las siguientes conversiones en tiempo real:

1. **Ronda Binaria (Base 2):** `01100011 01101000 01100001 01101001 01110010` -> **chair**
2. **Ronda Octal (Base 8):** `143 157 156 164 141 151 156 145 162` -> **container**
3. **Ronda Hexadecimal (Base 16):** `736c75646765` -> **sludge**

Comandos utilizados:
- Conexión: `nc fickle-tempest.picoctf.net 50496`

Al ingresar las tres palabras correctamente, el servidor validó el desafío y entregó la bandera.

## Bandera
`picoCTF{learning_about_converting_values_bf1F59A2}`