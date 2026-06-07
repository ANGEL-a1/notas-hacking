### Descripción del Reto

El reto `Mini RSA` expone una vulnerabilidad crítica en la implementación del algoritmo criptográfico RSA cuando se utiliza un **exponente de cifrado demasiado pequeño** ($e = 3$) junto con un relleno (_padding_) insuficiente. Aunque el módulo $N$ es un número colosal de uso estándar, la debilidad matemática permite recuperar el texto plano original sin necesidad de factorizar $N$ en sus componentes primos $p$ y $q$.

### Análisis Matemático del Ataque (Raíz Cúbica)

En el protocolo RSA estándar, la operación de cifrado de un mensaje $M$ se define mediante la fórmula:

$$C = M^e \pmod N$$

Normalmente, el valor de $M^e$ supera por mucho el tamaño del módulo $N$, provocando que la operación de residuo modular (`mod`) "envuelva" y disperse los bits del número de forma destructiva. Sin embargo, la descripción del reto aclara que el texto plano fue rellenado de tal forma que $M^e$ es **apenas un poco más grande** que $N$.

Debido a esto, podemos plantear la ecuación lineal original omitiendo la reducción modular:

$$M^3 = C + k \cdot N$$

Donde $k$ es un número entero pequeño. Si iteramos probando valores secuenciales para $k$ ($0, 1, 2, \dots$), llegará un punto en el que la suma de $C + k \cdot N$ equivalga a una **raíz cúbica perfecta** exacta. Al encontrar ese punto, la raíz cúbica del resultado nos dará de forma directa el mensaje original $M$.


### La Flag 

```
picoCTF{e_sh0u1d_b3_lArg3r_92f4d5a5}
```