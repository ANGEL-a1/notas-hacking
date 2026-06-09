# Scavenger Hunt

## Descripción del Reto
Este reto de nivel fácil (50 puntos) pertenece a la categoría de Explotación Web y consiste en una auditoría de reconocimiento pasivo y enumeración de archivos de código fuente y archivos de configuración del lado del servidor. El objetivo es recopilar fragmentos dispersos de la bandera analizando los comentarios de desarrollo, las hojas de estilo y los archivos de directivas estándar que suelen quedar expuestos por malas prácticas de despliegue web.

## Análisis de Archivos de Configuración y Fugas de Información
Durante el desarrollo y despliegue de aplicaciones web, es común que se filtren datos sensibles en archivos accesibles al público si no se configuran correctamente las restricciones de lectura:
* **Comentarios en Código (HTML/CSS)**: Práctica insegura donde los desarrolladores dejan notas o credenciales incrustadas en el código frontend.
* **robots.txt**: Archivo de texto utilizado para indicarle a los rastreadores web (crawlers) qué directorios no deben indexar. A menudo revela rutas ocultas a los atacantes.
* **.htaccess**: Archivo de configuración a nivel de directorio utilizado por el servidor web Apache para controlar contraseñas, redirecciones y accesos.
* **.DS_Store**: Archivo oculto creado automáticamente por los sistemas operativos macOS para almacenar metadatos de visualización de las carpetas. Su exposición permite mapear la estructura interna del proyecto.

## Proceso de Reconstrucción (Enumeración Web)
Para resolver el desafío, se realizó un proceso secuencial de inspección de recursos en el servidor web:
* **Parte 1**: Se inspeccionó el código fuente HTML de la página raíz, localizando el primer fragmento en un comentario de bloque (`picoCTF{t`).
* **Parte 2**: Se accedió al recurso `mycss.css` referenciado en el frontend, extrayendo el segundo fragmento al final de las reglas de estilo (`h4ts_4_l0`).
* **Parte 3**: Siguiendo la pista del archivo `myjs.js` sobre indexación, se consultó el archivo `/robots.txt`, revelando la tercera sección de la flag (`t_0f_pl4c`).
* **Parte 4**: La directiva de Apache del paso previo llevó a la consulta del archivo de configuración `/.htaccess`, obteniendo el cuarto fragmento (`3s_2_lO0k`).
* **Parte 5**: La pista final sobre el uso de infraestructura Apple permitió deducir la existencia del archivo de metadatos Mac `/.DS_Store`, el cual contenía el cierre definitivo de la estructura (`_9588550}`).

## Flag Obtenida:

picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_9588550}