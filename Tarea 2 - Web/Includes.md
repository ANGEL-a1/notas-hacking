# Includes

## Descripción del Reto
Este reto de nivel básico (100 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Explora los principios fundamentales de la auditoría de aplicaciones web, enfocándose en la inspección de archivos externos y la mala práctica de dejar comentarios con información sensible (*Information Disclosure*) en los recursos del lado del cliente.

## Análisis Técnico (Client-Side Source Code Inspection)
Cuando un navegador web procesa una dirección URL, no solo descarga el documento estructurado principal (`index.html`), sino que realiza peticiones asíncronas adicionales para cargar los recursos asociados que definen la lógica y la presentación de la página. Estos componentes externos comúnmente se dividen en:
1. **Hojas de Estilo en Cascada (CSS)**: Archivos `.css` responsables del diseño estático y la maquetación visual.
2. **Scripts de JavaScript (JS)**: Archivos `.js` encargados del comportamiento dinámico e interactividad en el entorno del cliente.

* **La Vulnerabilidad**: Todo el código transferido al navegador del cliente (HTML, CSS, JS) es públicamente accesible. El almacenamiento de secretos, llaves o banderas dentro de comentarios de desarrollo (`/* ... */` en CSS o `// ...` en JS) representa una falla crítica de divulgación de información, ya que los desarrolladores suelen asumir erróneamente que los archivos secundarios no son examinados a fondo.

## Proceso de Reconstrucción
1. Se accedió al sitio web del reto provisto por la instancia de la plataforma.
2. Se abrieron las Herramientas de Desarrollador del navegador (*DevTools*) presionando la tecla `F12` y se navegó a la pestaña **Sources** (Fuentes) para inspeccionar el árbol de dependencias cargadas.
3. Al examinar el archivo de estilos **`style.css`**, se localizó un bloque de comentario al final que exponía la primera sección de la bandera:

# Flag

   picoCTF{1nclu51v17y_1of2_f7w_2of2_df589022}