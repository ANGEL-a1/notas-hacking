# Inspect HTML

## Descripción del Reto
Este reto de nivel básico (100 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Se centra en comprender el uso del inspector de elementos del navegador web y auditar la estructura principal de una página para identificar malas prácticas asociadas con comentarios de desarrollo expuestos en el lado del cliente.

## Análisis Técnico (Client-Side DOM Inspection)
El código de marcado estructurado HTML es el componente base que un servidor web transfiere al navegador del usuario para renderizar visualmente el contenido de una página. Debido a que el protocolo HTTP/S transmite estos archivos de manera íntegra para que sean interpretados a nivel local por el cliente, todo su contenido es legible de manera pública.

* **La Vulnerabilidad**: Durante las fases de desarrollo o depuración, es común que los programadores inserten anotaciones técnicas, recordatorios o credenciales temporales utilizando la sintaxis de comentarios de HTML (``). Al pasar el sitio a entornos de producción sin una fase previa de limpieza o minificación, estos comentarios se vuelven accesibles de forma pública. Aunque no se despliegan de forma visual en la interfaz gráfica, el *Document Object Model* (DOM) del navegador los retiene intactos.
* **La Solución**: Basta con invocar las herramientas de desarrollo nativas del navegador para examinar directamente el código fuente crudo enviado por el servidor, puenteando cualquier restricción visual impuesta por las reglas de estilo de la página.

## Proceso de Reconstrucción
1. Se accedió al portal web asignado por la instancia activa del reto.
2. Se procedió a examinar la estructura base del sitio web utilizando la combinación de teclas `Ctrl + U` para forzar el despliegue del código fuente plano de la página en una pestaña independiente del navegador.
3. Se realizó una auditoría visual sobre el documento HTML buscando bloques sintácticos que hicieran uso de etiquetas de comentario.
4. Al final de la estructura interna del archivo, justo debajo de los elementos principales del cuerpo de la página, se localizó la bandera completa oculta en una línea de anotación
## Flag Obtenida:

picoCTF{1n5p3t0r_0f_h7ml_fd5d57bd}