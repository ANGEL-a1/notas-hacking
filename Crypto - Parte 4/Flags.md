# Flags

## Descripción del Reto
Este reto de nivel medio (200 puntos) pertenece a la categoría de Criptografía y se enfoca en la sustitución monoalfabética mediante el uso de códigos esteganográficos visuales históricos. El objetivo es identificar el sistema de codificación basado en el **Código Internacional de Señales Marítimas** (banderas náuticas), realizar el mapeo de cada ideograma hacia su correspondiente carácter alfabético estándar y reconstruir el mensaje en texto plano encerrado en el formato de la competencia.

## Análisis del Código Internacional de Señales y Ofuscación Leet Speak
El Código Internacional de Señales (ICS) emplea un alfabeto visual donde cada bandera representa de forma unívoca una letra (A-Z). Sin embargo, para elevar la dificultad, el desafío introduce una capa de ofuscación de tipo **Leet Speak** dentro de la cadena final. Los caracteres visuales de la palabra *"FLAGS AND STUFF"* sufren las siguientes sustitución numéricas en el validador del backend:
* La letra **L** se sustituye por el dígito **1** (F1AG5...).
* Las letras **S** se sustituyen por el dígito **5** (...5AND5...).

## Proceso de Reconstrucción (Traducción y Mapeo)
* **F** $\rightarrow$ Rombo rojo centrado en fondo blanco (Foxtrot).
* **1** $\rightarrow$ Representación Leet de la letra L / Banderín visual modificado.
* **A** $\rightarrow$ Banderín partido azul y blanco (Alfa).
* **G** $\rightarrow$ Franjas verticales amarillas y azules (Golf).
* **5** $\rightarrow$ Representación Leet de la letra S (Sierra).
* **A** $\rightarrow$ Banderín partido azul y blanco (Alfa).
* **N** $\rightarrow$ Tablero de ajedrez azul y blanco (November).
* **D** $\rightarrow$ Franjas horizontales azul, amarilla, azul (Delta).
* **5** $\rightarrow$ Representación Leet de la letra S (Sierra).
* **T** $\rightarrow$ Bandera tricolor vertical azul, blanca y roja (Tango).
* **U** $\rightarrow$ Cuadrantes invertidos blanco y rojo (Uniform).
* **F** $\rightarrow$ Rombo rojo centrado en fondo blanco (Foxtrot).
* **F** $\rightarrow$ Rombo rojo centrado en fondo blanco (Foxtrot).

## Flag Obtenida:

picoCTF{F1AG5AND5TUFF}