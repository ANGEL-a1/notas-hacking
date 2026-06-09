# dont-use-client-side

## Descripción del Reto
Este reto de nivel introductorio (100 puntos) pertenece a la categoría de Explotación Web y demuestra el riesgo de seguridad que implica confiar en el entorno del cliente (*Client-Side Validation*) para controlar el acceso a funciones restrictivas. El desafío expone un portal de autenticación que valida las credenciales de entrada utilizando funciones JavaScript expuestas en el código fuente de la página.

## Análisis de Vulnerabilidad (Bypass de Validación en Cliente)
La arquitectura de aplicaciones web seguras dicta que cualquier control de acceso o validación de secretos de autenticación debe procesarse estrictamente en el servidor (*Server-Side*). El código del cliente es intrínsecamente inseguro debido a que el usuario mantiene control absoluto sobre el DOM y los scripts en ejecución.
* **Falla de Lógica**: Al auditar el código fuente del portal web mediante las herramientas de desarrollo (*DevTools*), se identificó la función de JavaScript `verify()`. Esta rutina realiza comparaciones de subcadenas (`substring`) desordenadas de longitud fija (`split = 4`) evaluando la contraseña directamente contra fragmentos hardcodeados de la bandera en texto plano.

## Proceso de Reconstrucción
Se extrajeron secuencialmente las condicionales aritméticas del script ordenando los índices de los bloques en función del multiplicador de la variable `split` de menor a mayor (de 0 a split * 8):
1. `(0, split)` $\rightarrow$ `pico`
2. `(split, split*2)` $\rightarrow$ `CTF{`
3. `(split*2, split*3)` $\rightarrow$ `no_c`
4. `(split*3, split*4)` $\rightarrow$ `lien`
5. `(split*4, split*5)` $\rightarrow$ `ts_p`
6. `(split*5, split*6)` $\rightarrow$ `lz_2`
7. `(split*6, split*7)` $\rightarrow$ `eb02`
8. `(split*7, split*8)` $\rightarrow$ `b45}`

## Flag Obtenida:
picoCTF{no_clients_plz_2eb02b45}