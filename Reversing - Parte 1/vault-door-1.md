### Descripción del Reto

Este reto nos presenta un mecanismo de validación de contraseña implementado en Java (`VaultDoor1.java`). El objetivo es realizar ingeniería inversa sobre el código fuente para reconstruir la cadena de texto que desbloquea la bóveda, la cual corresponde a la bandera (`flag`) del reto.

### Análisis del Código Fuente

Al revisar el método `checkPassword(String password)`, observamos que el programa realiza las siguientes validaciones:

1. Verifica que la longitud de la contraseña introducida sea exactamente de **32 caracteres**.

2. Utiliza el método `.charAt(índice)` de Java para comprobar que cada posición de la cadena coincida con un carácter específico.


El desarrollador intentó ofuscar la contraseña colocando las comprobaciones de los índices de forma **completamente desordenada** dentro del condicional `if`.

### Proceso de Reconstrucción (De-ofuscación)

Para resolverlo, simplemente mapeamos cada índice (`0` al `31`) con el carácter que le corresponde en el código:

- `0` $\rightarrow$ `'d'`
- `1` $\rightarrow$ `'3'`
- `2` $\rightarrow$ `'5'`
- `3` $\rightarrow$ `'c'`
- `4` $\rightarrow$ `'r'`
- `5` $\rightarrow$ `'4'`
- `6` $\rightarrow$ `'m'`
- `7` $\rightarrow$ `'b'`
- `8` $\rightarrow$ `'l'`
- `9` $\rightarrow$ `'3'`
- `10` $\rightarrow$ `'_'`
- `11` $\rightarrow$ `'t'`
- `12` $\rightarrow$ `'H'`
- `13` $\rightarrow$ `'3'`
- `14` $\rightarrow$ `'_'`
- `15` $\rightarrow$ `'c'`
- `16` $\rightarrow$ `'H'`
- `17` $\rightarrow$ `'4'`
- `18` $\rightarrow$ `'r'`
- `19` $\rightarrow$ `'4'`
- `20` $\rightarrow$ `'c'`
- `21` $\rightarrow$ `'T'`
- `22` $\rightarrow$ `'3'`
- `23` $\rightarrow$ `'r'`
- `24` $\rightarrow$ `'5'`
- `25` $\rightarrow$ `'_'`
- `26` $\rightarrow$ `'a'`
- `27` $\rightarrow$ `'4'`
- `28` $\rightarrow$ `'d'`
- `29` $\rightarrow$ `'7'`
- `30` $\rightarrow$ `'3'`
- `31` $\rightarrow$ `'6'`


**Flag Obtenida:**

`picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_a4d736}`