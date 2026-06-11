# WebDecode

## Descripción del Reto
Este reto de nivel básico (50 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Se enfoca en el uso del inspector de elementos para la detección de fugas de información (*Information Disclosure*) en componentes del DOM y en la identificación de esquemas de codificación estándar como Base64 implementados erróneamente para intentar ocultar datos sensibles.

## Análisis Técnico (Information Disclosure & Base64 Encoding)
En el diseño de aplicaciones web, es común que se empaqueten múltiples recursos estáticos correlacionados (`.html`, `.css`, `.js`). Un fallo de seguridad habitual consiste en incrustar cadenas de datos confidenciales o flags dentro de atributos personalizados de etiquetas HTML (como propiedades `data-*` o nombres de atributos arbitrarios) asumiendo que el usuario común no interactuará con las herramientas de inspección.

* **La Vulnerabilidad**: El desarrollador incrustó la bandera codificada en Base64 dentro de un atributo HTML en una sección secundaria del portal. La codificación (Encoding) no debe confundirse con el cifrado (Encryption); mientras que el cifrado protege la confidencialidad mediante llaves secretas, la codificación únicamente altera el formato de representación binaria a texto usando un algoritmo público y reversible, permitiendo su recuperación inmediata sin requerir llaves asociadas.
* **La Solución**: Auditar la estructura jerárquica de etiquetas en los diferentes subdocumentos de la aplicación hasta aislar la propiedad codificada y revertir su formato en el espacio de trabajo local.

## Proceso de Reconstrucción
1. Se accedió a la página de inicio de la instancia web provista para el desafío.
2. Al examinar el menú de navegación, se detectó la presencia de rutas secundarias hacia los archivos `about.html` y `contact.html`.
3. Se inspeccionó el código fuente de la subpágina `about.html` mediante las herramientas de desarrollo del navegador (`F12`).
4. Dentro del cuerpo del documento, se descubrió una etiqueta `<section>` configurada con un atributo personalizado sospechoso llamado `notify_true`, el cual almacenaba una cadena alfanumérica con la estructura típica de un bloque Base64
5. Se extrajo la cadena alfanumérica y se procesó su reversión nativa en la terminal PowerShell invocando las clases de conversión de .NET Core, lo que decodificó los bytes originales y expuso la bandera en texto plano.

# Flag Obtenida

picoCTF{web_succ3ssfully_d3c0ded_07b91c79}