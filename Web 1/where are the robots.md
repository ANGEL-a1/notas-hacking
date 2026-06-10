# where are the robots

## Descripción del Reto
Este reto de nivel introductorio (100 puntos) pertenece a la categoría de *Web Exploitation* y aborda la fase de reconocimiento pasivo y descubrimiento de recursos ocultos mediante el análisis del archivo de configuración de rastreo del lado del servidor (`robots.txt`). El objetivo es identificar directorios restringidos para motores de búsqueda externos y acceder a ellos de forma directa.

## Análisis Técnico (Auditoría de Archivos de Exclusión de Bots)
El archivo `robots.txt` es un estándar utilizado por los administradores de sistemas para regular el comportamiento de los web crawlers. Configurar directivas de restricción (`Disallow:`) sobre rutas críticas o directorios de desarrollo sin implementar controles de autenticación del lado del servidor (*Server-Side Access Control*) constituye una falla de divulgación de información (*Information Disclosure*), exponiendo la superficie de ataque del sitio web de manera pública.

## Proceso de Reconstrucción
1. Se navegó hacia la raíz del servidor web solicitando explícitamente el recurso `/robots.txt`.
2. Se auditó el archivo de texto plano identificando la siguiente directiva de exclusión configurada por el desarrollador

# Flag

picoCTF{ca1cu1at1ng_Mach1n3s_cc6b1}