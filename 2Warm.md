# 2Warm

## Descripción del Reto
¿Se puede convertir el número 42 (base 10) a binario (base 2)?

## Solución
Para resolver este reto, realicé la conversión del número decimal 42 a binario. Esto se logra dividiendo el número entre 2 de manera consecutiva y tomando los residuos de abajo hacia arriba:

* 42 / 2 = 21 (Residuo 0)
* 21 / 2 = 10 (Residuo 1)
* 10 / 2 = 5  (Residuo 0)
* 5 / 2 = 2   (Residuo 1)
* 2 / 2 = 1   (Residuo 0)
* 1 / 2 = 0   (Residuo 1)

El resultado obtenido es `101010`.

## Bandera
`picoCTF{101010}`