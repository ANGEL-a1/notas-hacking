# Codebook 
## 📝 Descripción del Reto
El desafío consiste en ejecutar un script de Python (`code.py`) encargado de realizar una operación de descifrado simétrico XOR sobre una cadena de bytes predefinida (`flag_enc`). Para lograrlo con éxito, el programa debe leer un archivo de texto complementario (`codebook.txt`) posicionado en su mismo directorio de trabajo, el cual actúa como un diccionario indexado para reconstruir la contraseña de descifrado.

* **Categoría:** General Skills
* **Dificultad:** Easy (20 puntos)
* **Concepto Clave:** Manipulación de Archivos / Indexación de Cadenas / Cifrado XOR

---

## 📐 Análisis del Código y Solución Estática

El programa almacena los caracteres codificados individualmente en un arreglo y extrae de forma dinámica los componentes de la contraseña utilizando los índices del archivo de texto:

``
Contenido de codebook.txt: azbycxdwevfugthsirjqkplomn

## FLAG
`picoCTF{c0d3b00k_455157_197a982c}`