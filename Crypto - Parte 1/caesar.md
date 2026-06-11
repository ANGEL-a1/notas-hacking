# caesar

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 100 puntos) pertenece a la categoría de Criptografía (*Cryptography*). Requiere el análisis y la ruptura mediante un ataque de fuerza bruta por análisis rotacional sobre un criptograma basado en el Cifrado César clásico.

## Análisis Técnico (Exhaustive Shift Key Search)
A diferencia de esquemas con rotaciones fijas predeterminadas (como ROT13), un Cifrado César genérico sobre el alfabeto inglés posee un espacio de claves sumamente reducido: exactamente $26 - 1 = 25$ llaves posibles de desplazamiento matemático.

El flujo del archivo de entrada `data.enc` exponía la firma de control `picoCTF{...}` intacta, aislando el proceso de cifrado únicamente al string interior de las llaves (`furvvlqjwkhuxelfrqslandktj`). 

La función matemática inversa aplicada para la recuperación del texto en claro es:
$$\text{Decriptar}(c) = (c - \text{shift}) \pmod{26}$$

Donde se itera la variable $\text{shift}$ en el rango $[1, 25]$ hasta que el espacio de estados devuelva una cadena con entropía lingüística reconocible (gramática inglesa legítima).

## Proceso de Reconstrucción
1. Se aisló el criptograma interno provisto por el reto: `furvvlqjwkhuxelfrqslandktj`.
2. Se programó un script en Python para automatizar el ataque de fuerza bruta, barriendo de forma indexada los 25 desplazamientos modulares sobre la tabla ASCII.
3. El script volcó el espacio completo de combinaciones en la consola.
4. Mediante inspección visual del reporte, se determinó que la rotación número 3 (**ROT-03**) rompía la opacidad del criptograma, revelando la frase legítima *'crossing the rubicon'* concatenada con el hash dinámico de la sesión.

## Flag Obtenida:
picoCTF{crossingtherubiconpixkahqg}