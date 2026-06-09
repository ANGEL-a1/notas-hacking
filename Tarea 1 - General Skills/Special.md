# Special

## Descripción del Reto

Este reto de nivel medio (300 puntos) consiste en evadir un cascarón restringido (_Restricted Shell_) apodado "Special". Esta terminal intercepta cualquier comando, aplica un corrector ortográfico y capitaliza la primera letra de cada palabra de forma automática, convirtiendo comandos de sistema comunes en fallos de ejecución. Además, implementa un filtro estricto que impide el uso de rutas absolutas al bloquear cualquier entrada cuyo comando inicial comience con la diagonal `/`. El objetivo es burlar estas restricciones para lograr leer el archivo de la bandera (`flag.txt`) ubicado dentro del subdirectorio `blargh`.

## Análisis de Evasión de Filtros

En sistemas Unix/Linux, los entornos de ejecución restringidos o supervisados por scripts de filtrado de texto pueden ser evadidos mediante la inyección sintáctica y el uso de variables. Para lograr esta evasión se utilizan los siguientes conceptos: Asignación de Variables de Entorno (variable=valor comando): Permite evadir los filtros que analizan únicamente el primer token o palabra de la línea de comandos. Al asignar una variable ficticia al inicio de la línea, el corrector ortográfico actúa sobre el bloque de asignación y deja intacto el comando principal real. Además, al iniciar con caracteres alfabéticos y no con `/`, evade la validación que restringe rutas absolutas. Módulo os de Python (os.system): Permite interactuar de forma nativa con la shell real subyacente del sistema operativo desde un entorno interactivo independiente (`>>>`), lo que anula de forma permanente las interceptaciones y filtros del script supervisor del reto.

## Proceso de Reconstrucción (Evasión de Cascarón Restringido)

Para resolver el desafío, se analizó el comportamiento de la terminal "Special" interactuando con el puerto seguro remoto provisto a través de SSH: Se descartó la ejecución directa de comandos simples como ls o cat debido a que el script de control (Special.py) interceptaba y capitalizaba el primer término de cualquier comando alfabético simple, rompiendo su sintaxis. Se descartó el uso de rutas absolutas directas como /bin/ls o /bin/cat ya que el filtro de seguridad bloqueaba estrictamente el uso de diagonales iniciales arrojando excepciones personalizadas. Se ejecutó el bypass de capitalización inyectando un prefijo de variable de entorno para forzar la ejecución del intérprete interactivo de Python de forma segura mediante la instrucción placeholder=abc /usr/bin/python3. Se importó la biblioteca de interacción con el sistema operativo dentro del prompt interactivo de Python para listar de forma limpia el contenido del directorio oculto blargh. Se identificó que el contenido del archivo flag.txt alojado dentro del subdirectorio blargh contenía la estructura explícita de la bandera del reto.

# Flag Obtenida: 

picoCTF{5p311ch3ck_15_7h3_w0r57_f906e25a}