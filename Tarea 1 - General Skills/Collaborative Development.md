# Collaborative Development

## Descripción del Reto
Este reto profundiza en los conceptos de ramificación (branching) y colaboración en entornos controlados por el sistema de control de versiones Git. El objetivo es inspeccionar un repositorio local donde múltiples desarrolladores trabajaron en paralelo implementando características en ramas independientes. Se deben localizar, auditar y extraer los fragmentos de código aislados en cada rama para reconstruir de forma secuencial la bandera (flag) global del reto.

Análisis de Comandos de Ramificación
Para gestionar y navegar a través de flujos de desarrollo paralelo, Git implementa comandos críticos de administración de punteros:
1. `git branch -a`: Lista todas las ramas locales y referencias remotas del repositorio actual, permitiendo identificar líneas de desarrollo alternativas independientes de la rama principal (`main`/`master`).
2. `git checkout <rama>`: Alterna el entorno de trabajo actual hacia la rama especificada, modificando los archivos del directorio de trabajo para reflejar el estado del árbol de commits de dicho flujo.

Proceso de Reconstrucción (Auditoría Forense de Ramas)
Para resolver el desafío, se ejecutó un script automatizado en Python encargado de mapear e interrogar la base de datos de Git en la carpeta local `drop-in3`:

* Se ejecutó el listado de ramas, detectando tres ramas secundarias activas: `feature/part-1`, `feature/part-2` y `feature/part-3`.
* El script realizó un aislamiento de entorno mediante `git checkout` hacia cada una de las ramas de características.
* En cada iteración, se leyó el archivo de código fuente `flag.py` y se extrajeron las subcadenas parciales de la función `print()`.

### Fragmentos Extraídos:
* **Rama `feature/part-1`**: `picoCTF{t3@mw0rk_`
* **Rama `feature/part-2`**: `m@k3s_th3_dr3@m_`
* **Rama `feature/part-3`**: `w0rk_7ae8dd33}`

# Flag Obtenida:

picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_7ae8dd33}