# shark on wire 2 

## Enunciado
El desafío proporciona una captura de tráfico de red (`capture.pcap`). El objetivo es identificar el canal encubierto utilizado para exfiltrar la bandera y decodificar el mensaje.

## Análisis y Solución

1. **Reconocimiento del Tráfico:** Al inspeccionar el archivo `.pcap`, se observa un volumen masivo de paquetes UDP enviados hacia el puerto `5000` con mensajes de relleno como *"I really want to find some picoCTF flags"*.
2. **Descubrimiento del Canal Encubierto (Exfiltración):** Al analizar detalladamente los metadatos de red, los puertos de origen (*Source Ports*) de estas peticiones siguen un patrón numérico que inicia en el rango de los `5000`. Al restar `5000` a cada puerto de origen, los residuos resultantes equivalen a los valores decimales de caracteres de la tabla ASCII (ej. `5112 -> 112 = 'p'`).
3. **Automatización:** Se puede emplear un script de Python con la librería `scapy` para filtrar el tráfico UDP destinado al puerto 5000, extraer los puertos de origen, aplicar el desplazamiento matemático y reconstruir la flag de forma limpia:

```python
from scapy.all import rdpcap

packets = rdpcap('capture.pcap')
flag = ""

for pkt in packets:
    if pkt.haslayer('UDP') and pkt['UDP'].dport == 5000:
        src_port = pkt['UDP'].sport
        # Filtrar el desfase numérico para obtener el valor ASCII
        ascii_val = src_port - 5000
        if 32 <= ascii_val <= 126: # Rango de caracteres imprimibles
            flag += chr(ascii_val)

print(f"[+] Flag extraída: {flag}")
````

## Bandera

**🏆 Flag:** `picoCTF{p1LLf3r3d_data_v1a_st3g0}`