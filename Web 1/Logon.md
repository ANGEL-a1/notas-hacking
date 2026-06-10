# Logon

## Descripción del Reto
Este reto de nivel introductorio (100 puntos) pertenece a la categoría de *Web Exploitation* y aborda las fallas lógicas en los mecanismos de control de acceso basados en sesiones, específicamente la manipulación indebida de Cookies de autenticación en texto plano. El objetivo es evadir un formulario de inicio de sesión modificando los parámetros de identidad almacenados en el navegador para ingresar como un usuario privilegiado sin conocer su credencial legítima.

## Análisis de Vulnerabilidad (Manipulación de Cookies de Sesión)
Las cookies son vectores utilizados por las aplicaciones web para mantener el estado de una sesión HTTP. Sin embargo, delegar la lógica de privilegios de usuario directamente en valores editables por el cliente sin firmas criptográficas robustas (como tokens HMAC o JWT) constituye una vulnerabilidad crítica de Control de Acceso Roto (*Broken Access Control*).

* **Falla de Diseño**: Tras realizar un intento de autenticación con credenciales arbitrarias (ej. usuario y contraseña ficticios), el servidor web acepta la solicitud pero restringe el despliegue del secreto principal alegando falta de permisos de administrador. Al inspeccionar el almacenamiento local mediante la pestaña *Application* de las herramientas de desarrollador, se identificó la creación de una cookie explícita llamada `admin` con el valor inicial de `False`. El backend determina los privilegios evaluando directamente esta cadena booleana proveniente de la cabecera HTTP enviada por el cliente.

## Proceso de Reconstrucción
1. Se interceptó el almacenamiento de cookies del dominio en el cliente mediante las *DevTools* de Opera GX.
2. Se modificó manualmente el valor del parámetro manipulable `admin` cambiando el estado booleano de `False` a `True`.
3. Se alteró el parámetro `username` asignándole el identificador objetivo (`Joe`), evadiendo de esta forma la restricción de su formulario de inicio de sesión.
4. Se refrescó la solicitud HTTP, forzando al backend a procesar el nuevo estado alterado e inyectando de forma exitosa el acceso de administrador para revelar la bandera.

## Flag Obtenida:
picoCTF{th3_c0nsp1r4cy_l1v3s_4d184b0d}