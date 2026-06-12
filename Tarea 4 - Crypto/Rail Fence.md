# Rail Fence

### Enunciado:
Un tipo de cifrado por transposición es el cifrado Rail Fence (cifrado en zigzag). El payload fue encriptado utilizando este método con un total de 4 rieles (rails). El objetivo es reconstruir la matriz simétrica para recuperar el texto en claro.

---

## 🔍 Análisis Criptográfico y Solución

El cifrado Rail Fence no altera el valor de los caracteres individuales, sino que altera sus posiciones originales escribiendo el flujo de texto en un patrón oscilatorio (zigzag) a través de una profundidad fija de líneas horizontales para luego concatenar los datos fila por fila.

### 1. Datos del Desafío:
* **Texto Cifrado (Ciphertext):** `Ta _7N6D49hlg:W3D_H3C31N__A97ef sHR053F38N43D7B i33___N6`
* **Profundidad de Rieles:** 4

### 2. Automatización de Ingeniería Inversa (Python)
Se diseñó un algoritmo en Python que simula la matriz del zigzag original marcando las posiciones clave y rellenando los bloques secuenciales para leer el resultado siguiendo el flujo diagonal invertido.

```python
# Algoritmo de descifrado Rail Fence con profundidad K=4
# El texto claro recuperado fue el siguiente:
# WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_4A76B997
````

## 🏆 Flag Obtenida

**`picoCTF{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_4A76B997}`**