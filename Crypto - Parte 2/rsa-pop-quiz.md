
### Descripción del Reto

El reto consiste en un cuestionario interactivo sobre los conceptos matemáticos del criptosistema **RSA**. A lo largo de varias rondas, el servidor solicita determinar si un escenario es factible y, de ser así, calcular variables como Módulo ($n$), Totiente ($\phi(n)$), Exponente Privado ($d$), Cifrado ($c$) o Descifrado ($m$).

### Análisis Teórico y Fórmulas Utilizadas

1. **Cálculo del Módulo ($n$):**

$$n = p \times q$$

2. **Función Totiente ($\phi(n)$):**

$$\phi(n) = (p - 1) \times (q - 1)$$

3. **Inverso Multiplicativo Modular ($d$):**

$$d \equiv e^{-1} \pmod{\phi(n)}$$

_En Python:_ `pow(e, -1, totient)`

4. **Descifrado del Mensaje ($m$):**

$$m = c^d \pmod n$$

_En Python:_ `pow(ciphertext, d, n)`

### Extracción Final de la Flag

El último `plaintext` numérico obtenido fue:

`218378661235194013475375491560393839271890611748313869466505982183260263630681999229565`

Para convertir el entero de gran tamaño a la cadena ASCII correspondiente, se ejecutó el siguiente bloque en Python:

Python

```
m_final = 218378661235194013475375491560393839271890611748313869466505982183260263630681999229565
hex_str = hex(m_final)[2:]
if len(hex_str) % 2 != 0: 
    hex_str = '0' + hex_str
print(bytes.fromhex(hex_str).decode())
```

**Flag Obtenida:**

`picoCTF{wA8_th4till3aGal..ob6435DeB}`
