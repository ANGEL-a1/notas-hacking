# Blame Game

## Descripción del Reto
Este reto introduce el uso de herramientas de auditoría y forense de historial dentro del sistema de control de versiones Git. El objetivo es inspeccionar un repositorio local, analizar los metadatos de los commits realizados por diferentes colaboradores e identificar la identidad (nombre de usuario o correo electrónico) del autor responsable de introducir una modificación específica que impide el funcionamiento del programa, la cual constituye la bandera (flag) del reto.

Análisis de Comandos de Git
Para auditar repositorios y descubrir quién realizó modificaciones línea por línea o commit por commit, Git cuenta con dos comandos esenciales explicados en la documentación oficial de picoPrimer:
1. `git log`: Despliega el historial completo de confirmaciones en orden cronológico inverso, mostrando el hash del commit, el autor (nombre y correo) y la fecha.
2. `git blame <archivo>`: Muestra de forma detallada qué usuario modificó cada línea de un archivo específico y en qué commit lo hizo, siendo ideal para proyectos colaborativos.

Proceso de Reconstrucción (Forense de Repositorio)
Para resolverlo, se descargó el archivo comprimido del reto y se extrajeron sus componentes asegurando la preservación de los directorios ocultos del sistema:

* Se navegó hacia la carpeta raíz `challenge/home/ctf-player/drop-in` que aloja la base de datos oculta `.git`.
* Al no contar con un entorno interactivo SSH/Netcat funcional para correr el juego de búsquedas binarias, se optó por interrogar directamente la bitácora de control de versiones.
* Se ejecutó el comando `git log` filtrando la salida para aislar los metadatos del commit problemático.
* Se identificó que la firma del autor del commit contenía explícitamente el token del reto en su nombre de usuario.

# Flag Obtenida:

picoCTF{@sk_th3_1nt3rn_cfca95b2}