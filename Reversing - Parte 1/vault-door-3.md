## Solución: vault-door-3 (picoCTF)

### Descripción del Reto

En este reto, el mecanismo de validación de la contraseña en Java (`VaultDoor3.java`) implementa un algoritmo de ofuscación basado en **cuatro bucles `for` consecutivos**. Estos bucles mezclan las posiciones de la cadena original (`password`) dentro de un arreglo temporal (`buffer`). Al final, compara el resultado con la siguiente cadena estática:

`"jU5t_a_sna_3lpm15g64e_u_4_m1r74d"`

### Análisis de los Bucles y Tabla de Mapeo

El método `checkPassword(String password)` exige una longitud estricta de **32 caracteres**. Para realizar la ingeniería inversa, analizamos cómo cada bucle escribe en las posiciones del `buffer` (s) y despejamos el índice correspondiente de la contraseña original (`password`):

1. **Bucle 1 (`0` a `7`):** Mapeo directo. (password[i]=s[i]).

2. **Bucle 2 (`8` a `15`):** Mapeo inverso en espejo. (password[23−i]=s[i]).

3. **Bucle 3 (`16` a `31`, pares):** Mapeo entrelazado desde el extremo. (password[46−i]=s[i]).

4. **Bucle 4 (`31` a `17`, impares en reversa):** Mapeo directo en posiciones impares. (password[i]=s[i]).


A continuación se muestra la tabla de seguimiento estricta ordenando el resultado final desde el índice `0` hasta el `31` de la contraseña original:

|Índice Original (`password`)|Origen del Carácter|Índice en el `buffer` (s)|Carácter Correspondiente|
|---|---|---|---|
|**0 al 7**|Bucle 1 (Directo)|`0` al `7`|**jU5t_a_s**|
|**8**|Bucle 2 (Espejo: 23−15)|`15`|**1**|
|**9**|Bucle 2 (Espejo: 23−14)|`14`|**m**|
|**10**|Bucle 2 (Espejo: 23−13)|`13`|**p**|
|**11**|Bucle 2 (Espejo: 23−12)|`12`|**l**|
|**12**|Bucle 2 (Espejo: 23−11)|`11`|**3**|
|**13**|Bucle 2 (Espejo: 23−10)|`10`|**_**|
|**14**|Bucle 2 (Espejo: 23−9)|`9`|**a**|
|**15**|Bucle 2 (Espejo: 23−8)|`8`|**n**|
|**16**|Bucle 3 (Par: 46−30)|`30`|**4**|
|**17**|Bucle 4 (Impar Directo)|`17`|**g**|
|**18**|Bucle 3 (Par: 46−28)|`28`|**r**|
|**19**|Bucle 4 (Impar Directo)|`19`|**4**|
|**20**|Bucle 3 (Par: 46−26)|`26`|**m**|
|**21**|Bucle 4 (Impar Directo)|`21`|**_**|
|**22**|Bucle 3 (Par: 46−24)|`24`|**4**|
|**23**|Bucle 4 (Impar Directo)|`23`|**_**|
|**24**|Bucle 3 (Par: 46−22)|`22`|**u**|
|**25**|Bucle 4 (Impar Directo)|`25`|**_**|
|**26**|Bucle 3 (Par: 46−20)|`20`|**e**|
|**27**|Bucle 4 (Impar Directo)|`27`|**1**|
|**28**|Bucle 3 (Par: 46−18)|`18`|**6**|
|**29**|Bucle 4 (Impar Directo)|`29`|**7**|
|**30**|Bucle 3 (Par: 46−16)|`16`|**5**|
|**31**|Bucle 4 (Impar Directo)|`31`|**d**|

**Flag Obtenida:** `picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_e1675d}`