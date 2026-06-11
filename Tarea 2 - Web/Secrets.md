# Secrets

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 200 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Se centra en la vulnerabilidad de exposición de directorios ocultos (*Directory Traversal / Information Disclosure*), demostrando cómo el rastreo recursivo de recursos en el código fuente del cliente permite descubrir estructuras jerárquicas anidadas que el desarrollador intentó ocultar por obsolescencia o falta de enlaces visibles en la interfaz principal.

## Análisis Técnico (Hidden Directory Disclosure)
Un error crítico en la arquitectura de despliegue web es asumir que un recurso, archivo o subdirectorio es seguro o inaccesible simplemente porque no existen hipervínculos (`<a href="...">`) que apunten hacia él desde el index principal del sitio.

* **La Vulnerabilidad**: El servidor web aloja una estructura de carpetas anidadas en cascada (estilo "muñeca rusa"). Aunque estas rutas no están indexadas visualmente para el usuario común, los metadatos y las rutas relativas empleadas para cargar hojas de estilo (`.css`), scripts (`.js`) o recursos multimedia delatan la existencia de los directorios raíz en el backend.
* **La Solución**: Ejecutar un mapeo analítico del árbol de dependencias de la página web. Al inspeccionar de forma consecutiva las llamadas a recursos de cada subnivel, un auditor puede deducir la ruta absoluta y acceder de manera manual mediante la barra de direcciones del navegador hasta alcanzar la ubicación final del secreto.

## Proceso de Reconstrucción
1. Se accedió a la página principal de la instancia web del reto.
2. Al inspeccionar el código fuente (`Ctrl + U`), se detectó que los estilos CSS se importaban desde una subcarpeta no declarada en el menú:
}
   <link href="secret/assets/index.css" rel="stylesheet" />
}

3. Se manipuló la URL en el navegador para ingresar de forma manual al primer nivel oculto: `/secret/`.
    
4. Al auditar el código fuente de esta nueva sección, se localizó una segunda bifurcación de carpetas en la importación de dependencia
    ```
    <link rel="stylesheet" href="hidden/file.css" />
    ```

5. Se repitió el proceso de escalamiento accediendo a la URL: `/secret/hidden/`.

6. En el código fuente de este tercer nivel, se descubrió un formulario de inicio de sesión manual que exponía el último subdirectorio y el nombre del archivo final en un campo oculto:

    ```
    <input type="hidden" name="db" value="superhidden/xdfgwd.html" />
    ```

7. Se estructuró la ruta absoluta en el navegador web para solicitar el recurso de forma directa al servidor web:

    ```
    [http://saturn.picoctf.net](http://saturn.picoctf.net):XXXXX/secret/hidden/superhidden/xdfgwd.html
    ```

8. El servidor procesó la petición del archivo HTML e imprimió la bandera directamente en el cuerpo del documento.

## Flag Obtenida:

picoCTF{succ3ss_@h3n1c@10n_51b260fe}