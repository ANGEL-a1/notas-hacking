# WebNet1 

## Descripción 
El desafío proporciona una captura de tráfico de red (`capture.pcap`) con tráfico HTTPS cifrado y una llave privada RSA (`picopico.key`). El objetivo es descifrar el flujo TLS para recuperar la bandera oculta.

## Análisis y Solución

1. **Desencapsulado TLS:** Al igual que en el reto anterior, el tráfico del puerto 443 viaja cifrado con TLS v1.2. Se carga la llave privada RSA en Wireshark yendo a:
   `Edit > Preferences > Protocols > TLS > RSA keys list` e inyectando el archivo `picopico.key` para el puerto 443 y protocolo `http`.

2. **Evasión del "Rabbit Hole" (Bandera Falsa):**
   Al aplicar el filtro `http` y analizar las peticiones en texto plano, aparece de inmediato un encabezado HTTP personalizado que dice:
   `Pico-Flag: picoCTF{this.is.not.your.flag.anymore}`
   Esta cadena es un señuelo dejado por el autor para enviar una flag incorrecta.

3. **Extracción del Contenido Real:**
   Inspeccionando a fondo los objetos transmitidos en la sesión descifrada, se identifica la transferencia de un archivo de imagen llamado `vulture.jpg`. Al extraer los bytes de este elemento o inspeccionar el flujo de datos HTTP correspondiente, se localiza la bandera legítima oculta dentro de la estructura del archivo JPEG.

## Bandera
Flag: `picoCTF{honey.roasted.peanuts}`