## Binary Search

# Descripción del Reto
Este reto presenta un juego interactivo basado en consola implementado en Bash (guessing_game.sh). El programa selecciona un número aleatorio entero en un rango inclusivo de 1 a 1000 y limita al operador a un máximo de 10 intentos de adivinación. El objetivo es aplicar de manera estricta el algoritmo de búsqueda binaria para reducir el espacio de búsqueda de forma logarítmica y extraer la bandera (flag) del sistema de archivos remoto.

Análisis del Código Fuente
Al examinar el script de automatización del juego, se destacan las siguientes directivas de control:

1. **Generación del Objetivo:** Modula el valor pseudoaleatorio interno de la variable de entorno nativa de la shell limitándolo al rango deseado: `target=$(( (RANDOM % 1000) + 1 ))`.
2. **Inmunidad a Señales (Hardening):** Implementa el comando `trap` para interceptar y anular interrupciones por teclado (`SIGINT`, `SIGQUIT`, `SIGTSTP`), obligando al usuario a concluir el flujo lineal o agotar sus intentos sin poder colgar el proceso de forma interactiva.
3. **Persistencia Criptográfica:** Al validar el número correcto mediante la sentencia `else`, el flujo ejecuta la lectura e interpretación de un archivo de configuración JSON local invocando a la herramienta de filtrado `jq`: `flag=$(cat /challenge/metadata.json | jq -r '.flag')`.

Proceso de Reconstrucción (Optimización Algorítmica)
Para resolverlo, se estableció una sesión SSH remota omitiendo las técnicas de fuerza bruta o adivinación aleatoria, ejecutando en su lugar una búsqueda binaria pura ($O(\log n)$):

* Se calculó el punto medio inicial inyectando el valor fijo `500`.
* Se evaluó dinámicamente la respuesta condicional del flujo del juego ("Higher!" / "Lower!"), lo que permitió truncar el 50% del rango de posibilidades remanentes en cada iteración del ciclo `while`.
* Al converger en el valor entero exacto del objetivo, se desbloqueó la llamada del sistema que lee el archivo de metadatos, desplegando el token de la competencia.

# Flag Obtenida:

picoCTF{g00d_gu355_de9570b0}