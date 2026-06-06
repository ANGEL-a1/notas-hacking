### Descripción del Reto

El reto `HashingJobApp` consiste en una prueba de velocidad donde un servidor remoto exige calcular el hash **MD5** de múltiples cadenas de texto aleatorias de forma consecutiva. Si el usuario tarda más de unos pocos segundos en responder, la conexión se cierra automáticamente por tiempo de espera (_timeout_). El objetivo es aprender a automatizar interacciones con sockets y comprender la generación de hashes desde la línea de comandos o scripts.

### Análisis del Problema y Limitaciones

Al conectarse al servidor mediante `netcat`, este despliega un mensaje solicitando el hash de una palabra atrapada entre comillas simples:


```
Please md5 hash the text between quotes, excluding the quotes: 'Joan of Arc'
Answer:
```

#### El problema del copiado manual:

Intentar copiar la palabra, abrir una pestaña para calcular el hash con `echo -n "palabra" | md5sum` y regresar a pegar el resultado suele fallar debido al temporizador estricto del servidor. Además, el servidor exige resolver **3 palabras seguidas** de forma correcta para liberar la bandera. Por lo tanto, la mejor estrategia de resolución es la **automatización**.

### La Flag 


```
picoCTF{4ppl1c4710n_r3c31v3d_674c1de2}
```