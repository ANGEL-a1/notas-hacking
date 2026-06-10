# picobrowser

## Descripción del Reto
Este reto de nivel intermedio (200 puntos) pertenece a la categoría de Explotación Web y aborda la suplantación de identidad del cliente mediante la manipulación de cabeceras HTTP (*HTTP Header Injection/Spoofing*). El objetivo es evadir un filtro del lado del servidor que restringe el acceso al secreto basándose estrictamente en el identificador del navegador (*User-Agent*).

## Análisis de Vulnerabilidad (Suplantación de User-Agent)
La cabecera `User-Agent` proporciona información técnica sobre el navegador, el motor de renderizado y el sistema operativo del cliente. Validar privilegios o restringir contenido basándose únicamente en este parámetro constituye una falla lógica de confianza ciega en los datos del cliente, ya que cualquier paquete o cabecera HTTP generada saliendo del host puede ser interceptada y modificada arbitrariamente antes de llegar al backend.

## Proceso de Reconstrucción
1. Se analizó el mensaje de rechazo del servidor web, el cual reflejaba la cadena del *User-Agent* activa del navegador Opera GX.
2. Se abrieron las herramientas de desarrollo en el panel de *Network conditions*.
3. Se deshabilitó la configuración automática del agente de usuario por defecto del navegador.
4. Se inyectó una cadena personalizada forzando el valor a `picobrowser`.
5. Se revió la solicitud HTTP manteniendo el panel activo, evadiendo la regla de filtrado del servidor web y obteniendo la bandera en el DOM.

## Flag Obtenida:
picoCTF{p1c0_s3cr3t_ag3nt_fba5c48f}