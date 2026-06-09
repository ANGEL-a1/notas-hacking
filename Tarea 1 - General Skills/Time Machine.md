# Time Machine

## Descripción del Reto
Este reto aborda la inspección de metadatos de confirmación dentro del sistema de control de versiones Git. El objetivo es resolver un escenario donde un desarrollador dejó una nota recordatoria sobre su último trabajo, guardando dicha información directamente en el mensaje del commit en lugar del contenido de los archivos de texto. Se requiere auditar la bitácora de mensajes del repositorio para extraer la bandera (flag).

Análisis de Mensajes de Commit
En Git, cada vez que se consolida un cambio mediante una confirmación, se asocia un mensaje descriptivo que funciona como bitácora de desarrollo. Para examinar estos registros se utiliza el siguiente comando:
* `git log`: Despliega el historial de confirmaciones mostrando identificadores hash, datos del autor, marcas de tiempo y los mensajes de confirmación de texto plano adjuntos a cada estado del repositorio.

Proceso de Reconstrucción (Inspección de Bitácoras)
Para resolver el desafío, se analizó el entorno local del repositorio extraído bajo el directorio `drop-inT` mediante la automatización de consultas a la base de datos interna de Git:

* Se descartó la inspección de archivos individuales mediante comandos como `cat` o `type` debido a que el almacenamiento de la bandera no residía en el área de trabajo (Working Directory).
* Se ejecutó el volcado del historial filtrando la salida con el parámetro `--pretty=format:%s` para aislar exclusivamente los textos de los mensajes de confirmación.
* Se identificó que el mensaje del último commit registrado contenía la estructura explícita de la bandera del reto.

# Flag Obtenida:

picoCTF{t1m3m@ch1n3_b476ca06}