# Cookie Monster Secret Recipe

## Descripción del Reto
Este reto de nivel introductorio (*Easy*, 50 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Explora el concepto de almacenamiento inseguro de información confidencial (*Insecure Information Storage*) en las cookies del navegador del cliente, combinando técnicas de inspección de almacenamiento con decodificación de datos formateados en URL-Encode y Base64.

## Análisis Técnico (Insecure Information Storage)
Las cookies HTTP se diseñaron primordialmente para mantener estados de sesión o almacenar preferencias del usuario. 

* **La Vulnerabilidad**: Un fallo clásico en implementaciones web es almacenar secretos de la aplicación o banderas de verificación directamente en el espacio de almacenamiento del cliente de forma persistente. Al no aplicar un cifrado fuerte en el backend ni almacenar el secreto exclusivamente del lado del servidor, los datos quedan expuestos ante cualquier auditoría local.
* **Mecanismos de Representación**: Para que los datos viajen de forma segura en las cabeceras HTTP, caracteres de asignación como `=` se transforman mediante *URL-Encoding* a secuencias legibles (ej. `%3D`). Tras limpiar este formato, se expone un bloque codificado en Base64, el cual es completamente reversible.

## Proceso de Reconstrucción
1. Se navegó a la instancia principal del reto del Monstruo de las Galletas.
2. Al denegarse el acceso directo, se abrieron las Herramientas de Desarrollo (`F12`) y se accedió al gestor de persistencia local:
   * **Ruta**: `Application` -> `Storage` -> `Cookies`.
3. Se localizó una cookie activa bajo el nombre `secret_recipe` que contenía el siguiente string codificado:

   cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlcl9jMDBraWVzXzQ3MzZGNkNCfQ%3D%3D

4. Se identificó la presencia de `%3D%3D` al final de la cadena, procediendo a su conversión limpia a caracteres de relleno de Base64 (`==`).
5. Se ejecutó la decodificación de los bytes del string en un entorno de terminal local para recuperar el texto plano original en formato UTF-8, cuidando la variación de caracteres generada dinámicamente por la instancia.

## Flag Obtenida:

picoCTF{c00k1e_m0nster_l0ves_c00kies_4736F6CB}