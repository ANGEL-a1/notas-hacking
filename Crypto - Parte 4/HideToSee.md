# HideToSee

## Descripción del Reto
Este reto de nivel medio (100 puntos) pertenece a la categoría de Criptografía y propone un escenario híbrido que combina **Esteganografía** (ocultamiento de información en contenedores multimedia) y **Criptografía clásica** mediante el algoritmo simétrico **Atbash**. El objetivo es extraer un archivo de texto plano incrustado en los coeficientes de una imagen digital y posteriormente revertir el cifrado de sustitución reflejada para obtener el token de acceso.

## Análisis Tecnológico

### 1. Esteganografía con Steghide
El reto emplea ocultamiento en formato JPG. Herramientas como `steghide` explotan la redundancia de datos insertando bits confidenciales dentro de la frecuencia de la imagen sin alterar perceptiblemente su firma visual. La extracción se realizó empleando la herramienta web FutureBoy Steganographic Decoder sin contraseña (*null passphrase*).

### 2. Cifrado Atbash
El cifrado Atbash es un caso particular del cifrado afín con parámetros $\alpha = 25$ y $\beta = 25 \pmod{26}$. Funciona sustituyendo la $i$-ésima letra del alfabeto por la $(26-i)$-ésima letra. Al ser un cifrado involutivo, el mismo algoritmo se auto-recíproca para cifrar y descifrar:
$$f(x) = (25 - x) \pmod{26}$$

## Proceso de Reconstrucción
* **Falle 1 (Extracción)**: Se procesó la imagen del reto mediante el decodificador esteganográfico, exfiltrando la cadena de texto base enmascarada bajo el inverso del alfabeto: `krxlXOU{zgyzhs_xizxp_8z0uvwwx}`.
* **Fase 2 (Descifrado)**: Se aplicó un mapeo de índices inversos sobre los arreglos de caracteres ASCII, realizando los ajustes pertinentes en las colisiones de caracteres del hash para recuperar la estructura nativa formal del backend.

## Flag Obtenida:

picoCTF{atbash_crack_8a0feddc}