# Tab, Tab, Attack
# Descripción del Reto
Using tabcomplete in the terminal will add years to your life, esp. when dealing with long directory names and filenames.

## Solución
Para resolver este reto, se nos proporciona un archivo comprimido que contiene una estructura de directorios extremadamente profunda y con nombres complejos. El objetivo es navegar a través de estas carpetas hasta encontrar un archivo ejecutable.

La forma más eficiente de hacerlo en la terminal de Linux es utilizando la tecla **Tab** (tab-complete). Ejecutamos el comando de cambio de directorio y presionamos Tab repetidamente para que la terminal complete los nombres automáticamente:

`cd Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/`

Una vez dentro de la última carpeta, encontramos el archivo ejecutable `fang-of-haynekhtnamet`. Lo ejecutamos para obtener la bandera:

`./fang-of-haynekhtnamet`

Al ejecutar el binario, este imprime directamente la bandera en la terminal.

## Bandera
`picoCTF{l3v3l_up!_t4k3_4_r35t!_fc588427}`