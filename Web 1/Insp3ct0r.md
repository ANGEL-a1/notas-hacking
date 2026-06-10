# Insp3ct0r

## Descripción del Reto
Este reto básico (50 puntos) pertenece a la categoría de Explotación Web y sirve como introducción a la auditoría estática de recursos front-end. El objetivo es inspeccionar el código fuente desplegado en el cliente para recolectar tres fragmentos independientes de una bandera distribuidos a través de los archivos de estructura, estilo y lógica del sitio.

## Análisis Técnico (Auditoría de Recursos Front-End)
Las aplicaciones web modernas basan su renderización en el cliente mediante la triada fundamental del desarrollo web:
* **HTML (HyperText Markup Language)**: Define la estructura semántica del documento.
* **CSS (Cascading Style Sheets)**: Modula la presentación y diseño estético del DOM.
* **JavaScript**: Ejecuta los hilos de control dinámico y lógica del lado del cliente.

Es una falla común de configuración dejar comentarios de desarrollo o credenciales expuestas dentro de estos archivos, ya que cualquier recurso de este tipo transferido al navegador es completamente público y legible a través del inspector de elementos.

## Proceso de Reconstrucción
Se utilizaron las herramientas de desarrollo (*DevTools*) en Opera GX para auditar de forma estática las fuentes del dominio:
1. **HTML**: Localizado en la pestaña *Elements* como comentario estructural dentro del contenedor del DOM. (`Part 1: picoCTF{tru3_d3`)
2. **CSS**: Localizado al final del archivo de estilos `mycss.css` en la pestaña *Sources*. (`Part 2: t3ct1ve_0r_ju5t`)
3. **JavaScript**: Extraído de los comentarios finales del script independiente `myjs.js`. (`Part 3: _lucky?302945a7}`)

## Flag Obtenida:
picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?302945a7}