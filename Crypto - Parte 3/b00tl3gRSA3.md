## Descripción del Reto

El desafío presenta un entorno de criptografía RSA no convencional (**Multi-Prime RSA**). En lugar de utilizar únicamente dos números primos grandes (p y q), el módulo N está compuesto por una gran cantidad de factores primos pequeños y repetidos, lo que altera el cálculo del exponente privado d.

## 🛠️ Datos de la Instancia Sincronizada

- **Host:** `fickle-tempest.picoctf.net`

- **Port:** `53526`

- **Exponente Público (e):** `65537`

### Criptograma (c):

```
2177733846941061390160745351823429203746557496955727457596086882472230881784926289860654500215641309226047528655661810841860090798899423445854526396051573430973987351479761067696655330985997455928978710969902599040413199967280041988389589031697167760515744653323302202834062147420629665612820078668918875710205108380789993870995498051889417725
```

### Módulo (n):

```
14037816059848637328214509433402914025069078340838310085920009156974921665813718950299925874134173693168163578796282173628326153814659530398825385213627042326150136974820028975796608178351302962291670790499583101532978428054743197933153254867403498966387859024630495493568244041044014829058845079298162702880671358457451916027596606009159417609
```

## 📐 Análisis y Resolución Matemática

### 1. Factorización por Curvas Elípticas (ECM)

Al procesar el módulo n mediante el motor avanzado de **Alpertron**, se detectó que el compuesto cuenta con **17,179,869,184** divisores debido a la gran cantidad de repeticiones de factores primos basales pequeños. El motor de Alpertron derivó de forma directa el valor exacto de la función Totient de Euler (ϕ(n)) de 344 dígitos:


```
phi = 14037816020598823543445996768766468480811534104405526358178522452160723088216674364929451892421560723253673074397382331944228036021030350112464894651156746409973775991248454854143200031136142008341544697474134324484344584833791211164332644242220599577448632364759488622302324823222072662807515063593089583400818681303217596679585792000000000000
```

### 2. Rompimiento de RSA

Utilizando el decodificador de criptografía de **dCode**, se introdujeron las variables controladas c, e, n junto al intermediate value ϕ obtenido previamente.

La herramienta computó exitosamente el inverso modular para hallar la clave privada d:

d≡e−1(modϕ(n))

Y aplicó la exponenciación modular para recuperar el mensaje en texto plano (m):

m≡cd(modn)

Posteriormente, el flujo realizó un desempaquetado de bytes nativo (`unhex`), ignorando los caracteres nulos (`\x00`) agregados por el padding de la operación modular.

##  Flag 

```
picoCTF{too_many_fact0rs_3023548}
```