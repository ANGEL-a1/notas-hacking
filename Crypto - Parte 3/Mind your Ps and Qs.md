### Descripción del Reto

El reto `Mind your Ps and Qs` presenta un escenario criptográfico basado en el algoritmo RSA. El exponente público utilizado es estándar ($e = 65537$), pero el módulo clave $N$ posee una debilidad crítica: su longitud en bits es extremadamente baja (~136 bits). Esta falta de entropía rompe la seguridad del sistema, permitiendo la **factorización directa de $N$** en sus componentes primos componentes $p$ y $q$.

Además, el reto incluye una capa de complicación extra: el autor del desafío invirtió el orden de los caracteres del texto plano original antes de realizar el cifrado, obligando a realizar una reversión de la cadena tras el descifrado matemático.

### Análisis de la Vulnerabilidad y Desglose Matemático

En una implementación segura de RSA, el módulo $N$ debe ser un número compuesto de al menos 2048 bits para evitar que los algoritmos de factorización modernos puedan descomponerlo en un tiempo físicamente viable.

Al ser $N$ un número tan pequeño:

$$N = 948406957756830799684818171639547165784816468744946013083947881743680617123566349$$

Es posible descomponerlo utilizando bases de datos de computación distribuida (como Factordb). Al romper $N$ y conocer los primos $p$ y $q$, la estructura privada de RSA colapsa por completo, permitiendo calcular la función Totient de Euler $\phi(N)$ y el exponente privado de descifrado $d$:

1. $\phi(N) = (p - 1) \times (q - 1)$
    
2. $d = e^{-1} \pmod{\phi(N)}$
    
3. $M = C^d \pmod N$
    

###  La Flag 

```
picoCTF{sma11_N_n0_g0od_1dc7ae91}
```