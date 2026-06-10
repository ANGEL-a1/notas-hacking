# Picker I

## Descripción del Reto
Este reto de nivel intermedio (100 puntos) pertenece a la categoría de Ingeniería Inversa (*Reverse Engineering*) y explora fallas críticas de seguridad basadas en la ejecución dinámica de código interpretado. El objetivo consiste en explotar una entrada de usuario mal validada en el backend del servidor para desviar el flujo lógico del programa hacia una función restringida encargada de revelar los secretos del sistema.

## Análisis Técnico (Insecure Dynamic Execution & eval() Injection)
El script implementa un bucle de ejecución iterativo continuo controlado por una estructura `while(True)`. 

* **La Vulnerabilidad**: El programa captura la entrada del usuario mediante un prompt interactivo sin ningún tipo de saneamiento (*sanitization*) o lista blanca (*allowlist*). El backend procesa de forma directa la cadena de texto ingresada concatenándole paréntesis funcionales antes de pasarla al intérprete de código dinámico
# Flag
picoCTF{4_d14m0nd_1n_7h3_r0ugh_6e04440d}