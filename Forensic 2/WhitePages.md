# WhitePages

## Descripción
El desafío proporciona un archivo de texto que aparece completamente en blanco (`whitepages.txt`). El objetivo es descubrir la información oculta usando análisis forense digital sobre caracteres invisibles.

## Análisis y Solución

1. **Identificación del Canal Oculto:** Al inspeccionar el archivo a nivel binario o usar comandos como `xxd`, se detecta que el documento no está vacío, sino que contiene miles de caracteres invisibles compuestos por dos patrones específicos: espacios estándar (`0x20`) y espacios Unicode de ancho completo (`0xE2 0x80 0x83`).
2. **Interpretación Binaria:** Esta combinación se utiliza como un sistema binario encubierto (Esteganografía de Espacios en Blanco). Se mapea un tipo de espacio a un bit `0` y el otro a un bit `1`
3. **Automatización:** Se puede utilizar un script en Python para leer los bytes del archivo, mapear los espacios a código binario crudo y decodificar los bytes resultantes a texto plano:

```python
def decode_whitepages():
    with open('whitepages.txt', 'rb') as f:
        file_content = f.read()
    
    binary_str = ""
    for byte in file_content:
        if byte == 0x20:  # Espacio estándar
            binary_str += "1"
        elif byte == 0xe2:  # Inicio del espacio Unicode de ancho completo
            binary_str += "0"
        # Omitimos los bytes de continuación del carácter Unicode (0x80, 0x83)
    
    # Agrupar los bits en bloques de 8 y convertirlos a caracteres
    flag = ""
    for i in range(0, len(binary_str), 8):
        byte_chunk = binary_str[i:i+8]
        if len(byte_chunk) == 8:
            flag += chr(int(byte_chunk, 2))
            
    print(f"[+] Mensaje decodificado:\n{flag}")

decode_whitepages()
````

Al ejecutar el descifrado, la cadena binaria se traduce en texto plano, exponiendo la bandera del reto.

## Bandera

**🏆 Flag:** `picoCTF{not_all_spaces_are_created_equal_57203502a1f295faf0d8cf42a1d4c769}`