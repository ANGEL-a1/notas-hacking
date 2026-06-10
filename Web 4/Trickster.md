# Trickster

## Descripción del Reto
Este reto de nivel avanzado (300 puntos) pertenece a la categoría de Explotación Web y aborda la subida insegura de archivos (*Insecure File Upload*) combinada con la ejecución remota de código (*RCE*). El objetivo consiste en evadir las restricciones criptográficas y de extensión del backend para cargar una webshell funcional capaz de interactuar con el sistema operativo subyecente.

## Análisis Técnico (File Upload Bypass & RCE)
El servidor implementa validaciones basadas en la extensión permitida (`.png`) y la verificación de firmas de archivos de imagen (*Magic Bytes*). 

* **La Vulnerabilidad**: El mecanismo de verificación de extensiones es defectuoso al procesar archivos con extensiones compuestas (como `.png.php`), permitiendo que el servidor web interprete el archivo como código ejecutable en el lado del servidor mientras el filtro lo aprueba. Adicionalmente, la inyección de los caracteres de la firma mágica binaria (`PNG`) al inicio del archivo confunde al analizador, permitiendo la ejecución de comandos del sistema operativo mediante el parámetro estructurado `passthru($_GET["cmd"])`.

## Proceso de Reconstrucción
1. Se auditó la estructura de directorios utilizando el archivo `robots.txt`, localizando la carpeta de almacenamiento `/uploads/` y las directivas en `instructions.txt`.
2. Se construyó una webshell compacta en PHP con extensión doble `.png.php`, inyectando la firma de simulación de imagen al inicio del archivo de forma fragmentada en variables de PowerShell para evadir las firmas estáticas de Windows Defender local.
3. Se cargó exitosamente el archivo burlando los filtros de extensión y formato del backend.
4. Se invocó la webshell mediante la URL parametrizada consumiendo el comando `ls ../`, localizando el archivo confidencial con nombre aleatorio `GAZWIMLEGU2DQ.txt`.
5. Se ejecutó el comando `cat` sobre el recurso para realizar el volcado completo de la bandera.

## Flag Obtenida:
picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_03d1d548}