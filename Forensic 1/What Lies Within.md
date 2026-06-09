# What Lies Within

## Descripción del Reto
Este reto de nivel medio (150 puntos) pertenece a la categoría de Forense Computacional y aborda el estudio de la Esteganografía, específicamente la ocultación de flujos de texto dentro del dominio espacial de una imagen digital (`buildings.png`). El objetivo es extraer los bits de datos binarios incrustados en los componentes de color de los píxeles sin alterar la renderización visual del archivo contenedor.

## Análisis de Esteganografía LSB (Least Significant Bit)
La ocultación de datos en el bit menos significativo aprovecha las limitaciones del sistema visual humano. 
* Los píxeles de una imagen digital a color están constituidos por tres canales primarios independientes: **R**ojo, **V**erde y **A**zul (**RGB**). Cada componente se almacena empleando un byte (8 bits de profundidad).
* Al modificar de forma selectiva el bit menos significativo (Bit 0, el de menor peso matemático) de cada canal para almacenar flujos binarios externos, el valor numérico del color varía únicamente en una unidad (ej. de 255 a 254). Esta mínima alteración cromática resulta imperceptible para el ojo humano, permitiendo el transporte seguro de criptogramas de texto plano dentro de la trama gráfica.

## Proceso de Reconstrucción
Se implementó un script automatizado en Python empleando la biblioteca `Pillow` para iterar secuencialmente a través de las tuplas RGB de los píxeles, aislar los bits menos significativos con operaciones de máscara binaria, y agruparlos en bytes legibles

## Flag Obtenida:

picoCTF{h1d1ng_1n_th3_b1t5}