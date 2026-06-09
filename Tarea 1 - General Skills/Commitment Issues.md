# Commitment Issues

## Descripción del Reto
Este reto introduce el concepto fundamental de persistencia en los sistemas de control de versiones Git. El objetivo es inspeccionar un repositorio local donde un desarrollador escribió la bandera en un archivo de texto y posteriormente la eliminó mediante un nuevo commit, asumiendo erróneamente que la información ya no era accesible. Se debe auditar el baúl de metadatos del historial para recuperar la información borrada, la cual constituye la bandera (flag) del reto.

Análisis de Recuperación de Historial
Para examinar modificaciones históricas y recuperar estados anteriores del código, Git implementa los siguientes mecanismos esenciales:
1. `git log -p`: Despliega la bitácora cronológica de confirmaciones detallando el parche o "diff" de código introducido en cada una. Esto permite visualizar líneas agregadas (con el prefijo `+`) y líneas eliminadas (con el prefijo `-`).
2. `git checkout <hash_commit>`: Mueve el puntero de trabajo hacia un commit específico del pasado, restaurando temporalmente el estado exacto de los archivos en ese punto del tiempo.

Proceso de Reconstrucción (Recuperación Forense)
Para resolver el desafío, se analizó el repositorio local extraído en la carpeta `drop-in4` utilizando herramientas automatizadas de auditoría de logs:

* Se inspeccionó el árbol de commits con el fin de rastrear las confirmaciones previas al borrado.
* Se utilizó un filtro para examinar las diferencias de código (`diffs`) introducidas en los bloques del pasado.
* Se aisló una línea del historial que iniciaba con el operador de remoción (`-`), revelando que la cadena original del archivo contenía la bandera antes de ser sobreescrita con un archivo vacío o modificado.

# Flag Obtenida:

picoCTF{s@n1t1z3_30e86d36}