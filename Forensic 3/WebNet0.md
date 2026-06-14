# WebNet0 
## Enunciado
El desafío proporciona una captura de tráfico de red (`capture.pcap`) que contiene tráfico web cifrado y una llave privada RSA (`picopico.key`). El objetivo es descifrar el flujo TLS para recuperar la bandera oculta en la sesión HTTPS.
## Análisis y Solución

1. **Identificación del Cifrado:** Al abrir el archivo `capture.pcap` en Wireshark, se observa que la comunicación del puerto 443 viaja bajo el protocolo TLS v1.2, lo que hace que los datos de la aplicación web sean completamente ilegibles a simple vista debido al cifrado asimétrico.
2. **Carga de la Llave Maestra:** Para abrir la "caja fuerte" del tráfico, se introduce la llave privada proveída en el analizador de protocolos:
   - Navegar a: `Edit > Preferences > Protocols > TLS` (o SSL en versiones anteriores).
   - En la sección **RSA keys list**, hacer clic en *Edit...* y añadir una nueva fila.
   - Configurar el puerto en `443`, el protocolo en `http`, y seleccionar el archivo `picopico.key` en el apartado *Key File*.
3. **Desencapsulado y Extracción:** Al aplicar la llave, Wireshark descifra los paquetes en tiempo real, transformando el tráfico TLS a HTTP plano (mostrado en color verde). Al aplicar el filtro `http` y seleccionar `Follow > HTTP Stream` en el paquete de la petición/respuesta del servidor de AWS, se expone el texto claro de la conversación, revelando la flag dentro del flujo.

## Bandera
	Flag: `picoCTF{nongshim.shrimp.crackers}`