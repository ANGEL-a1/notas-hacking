# Roboto Sans

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 200 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Explora el concepto de exposición de archivos de configuración del servidor y fugas de información (*Information Disclosure*) a través de metadatos públicos en el archivo estático `robots.txt`, combinando técnicas de análisis de exclusión de indexado con decodificación de datos en formato Base64.

## Análisis Técnico (Information Disclosure & Base64 Obfuscation)
El archivo `robots.txt` es un recurso crítico situado en la raíz de cualquier servidor web público. Su propósito es guiar a los indexadores automáticos (*web crawlers*) especificando qué rutas o archivos no deben ser rastreados para motores de búsqueda mediante la directiva `Disallow`.

* **La Vulnerabilidad**: Un fallo de diseño clásico es usar el archivo `robots.txt` como un mecanismo de "seguridad por oscuridad" (*Security through obscurity*), asumiendo que las rutas listadas en él permanecerán ocultas. Al ser un archivo de acceso público irrestricto, un auditor de seguridad puede inspeccionarlo directamente para mapear el inventario de recursos confidenciales expuestos en el backend.
* **El Mecanismo de Ofuscación**: En este escenario específico, el desarrollador intentó ocultar las rutas críticas codificándolas en Base64 dentro del cuerpo de texto del archivo de configuración. La codificación Base64 únicamente altera la representación binaria a texto imprimible mediante un algoritmo público y reversible, permitiendo su recuperación inmediata mediante funciones de conversión nativas del lado del cliente.

## Proceso de Reconstrucción
1. Se accedió a la URL raíz de la instancia activa del reto provista por el contenedor.
2. Utilizando la barra de direcciones del navegador, se solicitó de manera directa el archivo estándar de exclusión de rastreo:

   [http://saturn.picoctf.net:62444/robots.txt](http://saturn.picoctf.net:62444/robots.txt)


3. Al analizar el contenido del archivo de texto plano, se aislaron dos cadenas alfanuméricas anómalas intercaladas con las directivas del sistema, las cuales presentaban la estructura y relleno (`==`) característicos del esquema Base64:

    - Cadena 1: `ZmxhZzEudHh0`

    - Cadena 2: `anMvbXlmaWxlLnR4dA==`

4. Se abrió un entorno local de terminal PowerShell y se invocaron los métodos de la clase `System.Convert` de .NET Core para revertir la codificación de ambos strings a texto plano (`UTF8`):

    ```[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("ZmxhZzEudHh0"))      # Salida: flag1.txt
    [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("anMvbXlmaWxlLnR4dA==")) # Salida: js/myfile.txt
    ```
    
5. Tras identificar los directorios ocultos, se utilizó la herramienta de línea de comandos `curl` (`Invoke-WebRequest`) con el parámetro `-UseBasicParsing` para forzar una petición HTTP directa hacia la ruta del script del servidor:

    ```
    curl [http://saturn.picoctf.net:62444/js/myfile.txt](http://saturn.picoctf.net:62444/js/myfile.txt) -UseBasicParsing
    ```

6. El servidor web resolvió la petición de manera exitosa y retornó la bandera de seguridad incrustada en texto plano dentro del archivo.

## Flag Obtenida:

picoCTF{Who_D03sN7_L1k5_90B0T5_22ce1f22}