# interencdec

## Descripción del Reto
Este reto inicial (*Easy*, 50 puntos) pertenece a la categoría de Criptografía (*Cryptography*). Introduce el concepto de encapsulamiento criptográfico secuencial (esquema de "Matrioshka"), requiriendo la ejecución encadenada de múltiples algoritmos de decodificación simétrica y fuerza bruta sobre máscaras de rotación.

## Análisis Técnico (Multi-Layer Decoding Pipeline)
El análisis forense del archivo binario `enc_flag` reveló tres capas consecutivas de ofuscación de datos:

1. **Capa 1 (Base64 Externo)**: Reconocible por el alfabeto utilizado y el padding de sufijo `==`. La decodificación inicial del flujo binario expuso un string formateado como un objeto de bytes nativo de Python (`b'...'`).
2. **Capa 2 (Base64 Interno)**: Al aislar el contenido interno de los bytes extraídos, se identificó un segundo bloque codificado en Base64. Al revertirlo, se obtuvo una cadena alfabética que conservaba la estructura geométrica de la bandera, pero con caracteres transpuestos (`wpcoPGS{...}`).
3. **Capa 3 (Cifrado César / ROT)**: El criptograma final presentaba un desplazamiento monoalfabético estático. Al realizar un ataque de fuerza bruta lineal probando los 25 espacios del módulo del alfabeto, se determinó que un desplazamiento **ROT-19** devolvía los caracteres al rango ASCII original de la firma `picoCTF`.

## Proceso de Reconstrucción
1. Se extrajo el payload codificado del archivo original: `YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6YzRNalV3YUcxcWZRPT0nCg==`.
2. Se programó un pipeline automatizado en Python para procesar el flujo de datos directamente en memoria RAM:
   * Aplicó `base64.b64decode()` sobre el bloque externo.
   * Limpió las cabeceras de formateo y aplicó una segunda decodificación Base64.
   * Ejecutó un bucle indexado de transposición de caracteres para evaluar la rotación del abecedario.
3. El motor interceptó el patrón válido `picoCTF` al procesar la rotación número 19, imprimiendo la llave limpia.

## Flag Obtenida:
picoCTF{caesar_d3cr9pt3d_78250afc}