# Power Cookie

## Descripción del Reto
Este reto de nivel intermedio (*Medium*, 200 puntos) pertenece a la categoría de Explotación Web (*Web Exploitation*). Se enfoca en la vulnerabilidad de control de acceso roto mediante la manipulación de parámetros de sesión (*Broken Access Control / Cookie Manipulation*), demostrando cómo el cliente puede alterar cookies de estado no firmadas criptográficamente para elevar privilegios de forma ilegítima en el backend.

## Análisis Técnico (Insecure Cookie Privilege Escalation)
Las cookies HTTP son mecanismos clave empleados por las aplicaciones web para almacenar datos de estado en el navegador del usuario y persistir configuraciones o identidades entre diferentes peticiones.

* **La Vulnerabilidad**: El fallo radica en una confianza ciega del lado del servidor (*Insecure Parameter Validation*). El sistema delega la verificación del rol del usuario (`Guest` vs. `Admin`) a una cookie local legible y modificable en texto plano, sin implementar firmas criptográficas (como tokens JWT firmados) ni validaciones del lado del servidor que impidan su alteración.
* **Mecanismo de Explotación**: Al interceptar el almacenamiento local de cookies a través del DOM o las herramientas de depuración, un atacante puede reescribir los valores booleanos o numéricos asignados a variables de control (ej. cambiar un flag de `0` a `1`). Al enviar la petición de actualización, el backend procesa el nuevo estado modificado y concede accesos administrativos inmediatos.

## Proceso de Reconstrucción
1. Se ingresó al portal web del desafío, interactuando con la función de acceso para usuarios invitados (*Guest*).
2. El sistema redirigió a la interfaz secundaria notificando la ausencia de privilegios de administración.
3. Se abrieron las Herramientas de Desarrollo del navegador (`F12`) y se navegó a la sección de almacenamiento local de cookies:
   * **Ruta**: `Application` -> `Storage` -> `Cookies` -> Dominio de la instancia activa.
4. Se inspeccionó la tabla de llaves y valores, aislando una cookie crítica inicializada por el backend:
   * **Nombre**: `isAdmin`
   * **Valor Inicial**: `0`
5. Se efectuó una edición manual directa sobre el DOM de la tabla de almacenamiento, sustituyendo el valor restrictivo `0` por el valor lógico de activación `1`.
6. Se procedió a refrescar el documento en el navegador (`F5`), forzando la transmisión de la cookie modificada dentro de las cabeceras de la petición HTTP.
7. El servidor web interpretó la estructura de la cookie modificada como válida, evadió la restricción de seguridad y desplegó la bandera en la interfaz principal.

## Flag Obtenida:
picoCTF{gr4d3_A_c00k13_5d2505be}