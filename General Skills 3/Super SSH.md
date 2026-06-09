## Super SSH

## Descripción del Reto
Este reto introduce el uso del protocolo SSH (Secure Shell) para el acceso seguro y remoto a sistemas basados en Linux. El objetivo es establecer una sesión interactiva remota utilizando credenciales específicas y un puerto de comunicación alternativo para obtener la bandera (flag) protegida en el servidor de destino.

Análisis del Código Fuente / Infraestructura
Al analizar los requerimientos de conexión proporcionados para el reto, se identifican los siguientes parámetros estructurados:

1. Protocolo de comunicación: `SSH` (Puerto por defecto 22, modificado para este despliegue).
2. Credenciales de acceso estáticas: Usuario (`ctf-player`) y contraseña (`83dcefb7`).
3. Endpoint de destino: Host (`titan.picoctf.net`) configurado en el puerto específico `61793`.

Proceso de Reconstrucción (Conexión Remota)
Para resolverlo, se omitió el puerto por defecto y se estructuró un comando SSH explícito en la terminal local para redirigir el tráfico hacia el socket remoto correcto:

* Se ejecutó el comando de red especificando el puerto mediante la bandera `-p 61793`.
* Se aceptó el intercambio de llaves criptográficas (fingerprint) del host remoto respondiendo afirmativamente con la palabra explícita `yes`.
* Se ingresaron las credenciales autenticando de manera exitosa la sesión para forzar el despliegue automático del token de la competencia.

# Flag Obtenida:

picoCTF{s3cur3_c0nn3ct10n_8969f7d3}