# SOAP

## Descripción del Reto
Este reto de nivel intermedio (100 puntos) pertenece a la categoría de Explotación Web y expone la vulnerabilidad clásica de Inyección de Entidades Externas XML (*XML External Entity - XXE*). El objetivo consiste en manipular una solicitud basada en el protocolo SOAP para forzar al parser XML del backend a leer recursos locales restringidos del sistema operativo (`/etc/passwd`).

## Análisis Técnico (XML External Entity - XXE)
El protocolo SOAP confía en estructuras de datos XML para el intercambio de mensajes. Cuando un backend recibe estas solicitudes y las procesa mediante un analizador XML (*XML Parser*) configurado incorrectamente (permitiendo directivas `DOCTYPE` y resoluciones `SYSTEM`), el sistema se vuelve vulnerable a inyecciones.

* **La Vulnerabilidad**: El servidor confía ciegamente en la estructura XML entrante. Si las etiquetas no coinciden de forma estricta con el esquema esperado (en este caso, requería estrictamente la etiqueta `<ID>` en mayúsculas), el backend genera un error 500. Al estructurar el payload respetando el esquema exacto e inyectando una entidad externa referenciando el sistema de archivos local (`file://`), el parser concatena el contenido del archivo dentro de la respuesta HTTP expuesta.

## Proceso de Reconstrucción
1. Se analizó el flujo de peticiones del portal web mediante la pestaña Network de las DevTools, identificando el envío del payload original `<?xml version="1.0" encoding="UTF-8"?><data><ID>2</ID></data>`.
2. Se construyó un script en Python utilizando la librería `requests` para replicar la petición apuntando al endpoint `/data`.
3. Se inyectó una definición de tipo de documento (DTD) declarando una entidad externa maliciosa apuntando a `/etc/passwd`.
4. El servidor procesó la entidad de forma nativa e inyectó los usuarios del sistema junto con la bandera en la respuesta HTTP expuesta en la consola de VS Code.

## Flag Obtenida:
picoCTF{XML_3xtern@l_3nt1t1ty_540f4f1e}