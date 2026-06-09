# Shark on wire 1

## Descripción del Reto
Este reto de nivel medio (150 puntos) pertenece a la categoría de Forense Computacional y aborda el análisis de tráfico de red empaquetado empleando archivos de extensión `.pcap`. El objetivo consiste en inspeccionar los diversos flujos de datos (*Streams*) de los protocolos de la capa de transporte para aislar un canal de comunicación específico que contiene los caracteres de la bandera en texto plano, evadiendo el tráfico basura inyectado.

## Análisis de Protocolos y Flujos UDP
A diferencia de TCP, el protocolo **UDP (User Datagram Protocol)** no está orientado a la conexión ni mantiene un control de flujo indexado. En entornos forenses, la reconstrucción de sesiones UDP se realiza agrupando los datagramas que comparten los mismos sockets (IP:Puerto origen y destino).
* **Tráfico Basura**: El archivo de captura presenta una inundación intencional de paquetes de descubrimiento SSDP (`M-SEARCH`), consultas de resolución LLMNR (`wpad`) y datagramas UDP con payloads aleatorios de relleno para generar entropía y dificultar los filtros de búsqueda globales.
* **Aislamiento del Objetivo**: Al auditar secuencialmente los flujos utilizando herramientas de filtrado, un flujo UDP específico destaca por transmitir el payload real de forma limpia hacia la dirección destino del host `10.0.0.12:8888`.

## Flag Obtenida:

picoCTF{StaT31355_636f6e6e}