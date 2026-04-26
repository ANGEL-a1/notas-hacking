El reto presenta un escenario de RSA donde el módulo $n$ es extremadamente grande, lo que hace imposible la factorización por métodos convencionales. Sin embargo, el exponente público es muy bajo ($e = 20$).

### Análisis y Solución

1. **Vulnerabilidad:** Se identificó un **Low Exponent Attack**. Cuando el exponente $e$ es pequeño y el mensaje $m$ no es muy largo, el valor cifrado $c = m^e \pmod{n}$ puede no haber superado el valor de $n$ (es decir, $m^e < n$).
    
2. **Método:** En lugar de buscar los factores primos $p$ y $q$, se aplicó el **Método de Newton** para encontrar la raíz $e$-ésima exacta del ciphertext $c$ en el conjunto de los números enteros.
    
3. **Implementación:** Se utilizó un script de Python con un algoritmo de búsqueda binaria/Newton para manejar la precisión de los números de gran tamaño (BigInts) sin depender de librerías externas como `gmpy2`.
    

### Resultado

- **Valor de m decodificado:** El número resultante se convirtió de hexadecimal a ASCII para revelar la bandera.
    
- **Flag:** `picoCTF{t1ny_e_2fe2da79}`