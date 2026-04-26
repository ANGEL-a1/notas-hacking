
## 1. Descripción
Este reto de criptografía de nivel fácil en picoCTF se basa en el sistema de cifrado RSA. El
objetivo es descifrar una bandera (flag) utilizando únicamente los valores de N (módulo) y e
(exponente público) proporcionados por una instancia remota.
Mensaje de la instancia:

● N:
14720817651680747357556386708944217823355147540717332083789484188300924
74247983577660427147462807135529066259646212394648727670987127440080776
2735177241802
● e: 65537
● Cyphertext:
76359820570671490737353949386571354563769737115008093929156142024104509
57633946033394509941452200031747168925060370404525818816808612809560607
206397981943
##  2. Solución
Al analizar los valores de N en múltiples peticiones, se identificó que el sistema tiene una falla
en la generación de números aleatorios (Weak PRNG). Esto provoca que diferentes módulos
compartan factores primos.
Pasos realizados:
-  Se recolectaron dos módulos distintos ($N_1$ y $N_2$) conectándose a la instancia
mediante nc.
-  Se utilizó el algoritmo de Euclides para encontrar el Máximo Común Divisor (MCD)
entre ambos módulos, lo que reveló el factor primo común p = 2.
-  Con el valor de p, se calculó q = N / p.
-  Se obtuvo el valor de phi (Φ = (p-1)*(q-1)) para calcular el exponente privado d (la
inversa modular de e).
-  Se descifró el mensaje utilizando la fórmula $m = c^d \pmod{N}$ y se convirtió el
resultado de hexadecimal a texto plano.
Código utilizado (nanosolve.py):
from math import gcd
# Datos de la instancia
n1 =
14720817651680747357556386708944217823355147540717332083789484188300
92474247983577660427147462807135529066259646212394648727670987127440

0807762735177241802
c1 =
76359820570671490737353949386571354563769737115008093929156142024104
50957633946033394509941452200031747168925060370404525818816808612809
560607206397981943
n2 =
25041213280922029779110049602555849883582451399126941311607751962375
78179938761341608726778122405302422237466512810839007155231927927520
6602708276932958834

e = 65537
p = gcd(n1, n2)
q = n1 // p
phi = (p - 1) * (q - 1)
d = pow(e, -1, phi)
m = pow(c1, d, n1)
h = hex(m)[2:]
if len(h) % 2 != 0: h = '0' + h
print(f"FLAG: {bytes.fromhex(h).decode()}")

## 3. Bandera (Flag)
`picoCTF{tw0_1$_pr!m3df98b648}`
