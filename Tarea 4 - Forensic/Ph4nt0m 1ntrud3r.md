# Ph4nt0m 1ntrud3r

## Descripción del Reto

Este reto de nivel fácil (50 puntos) pertenece a la categoría de **Forensics** y consiste en analizar un archivo de captura de tráfico de red (`myNetworkTraffic.pcap`) para identificar información oculta transmitida por un atacante.

La descripción proporciona una pista fundamental:

> **"Attacks were done in timely manner"**
> **"Time is essential"**

Esto indica que el orden cronológico de los paquetes es un elemento clave para reconstruir la información robada.

---

## Análisis del Tráfico de Red

El archivo `.pcap` fue inspeccionado utilizando herramientas de análisis de red como **Wireshark**.

Durante la revisión de los paquetes se observó que ciertos datos eran enviados en forma de cadenas codificadas en **Base64**. A simple vista los fragmentos no parecían contener información útil, sin embargo, la pista sobre el tiempo sugería que debían reconstruirse respetando el orden exacto en que fueron transmitidos.

Para ello se procedió a:

1. Filtrar los paquetes relevantes.

2. Extraer las cadenas codificadas.

3. Decodificar los valores Base64.

4. Ordenar los resultados utilizando los timestamps de los paquetes.

5. Concatenar los fragmentos obtenidos.


---

## Reconstrucción de la Bandera

Después de decodificar y ordenar los fragmentos según su marca temporal, se obtuvieron los siguientes segmentos:

```text
picoCTF
{1t_w4s
nt_th4t
_34sy_t
bh_4r_9
66d0bfb
}
```

Al unirlos en el orden correcto se reconstruye la bandera completa:

```text
picoCTF{1t_w4snt_th4t_34sy_tbh_4r_966d0bfb}
```

---

## Procedimiento Utilizado

### Filtrado de paquetes

Se revisó el tráfico en busca de paquetes que contuvieran datos codificados o transmisiones sospechosas.

### Decodificación

Los fragmentos encontrados estaban codificados en Base64, por lo que se realizó la conversión correspondiente para recuperar su contenido original.

### Ordenamiento temporal

La clave del reto fue respetar el orden cronológico de los paquetes utilizando los timestamps almacenados en la captura. Sin este paso los fragmentos aparecían desordenados y no era posible reconstruir el mensaje.

### Ensamblado

Finalmente, los fragmentos decodificados fueron concatenados siguiendo el orden temporal exacto hasta obtener la bandera.

---

## Flag Obtenida

```text
picoCTF{1t_w4snt_th4t_34sy_tbh_4r_966d0bfb}
```