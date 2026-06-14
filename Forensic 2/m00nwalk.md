# m00nwalk

## Descripción
El desafío proporciona un archivo de audio con un sonido estridente y repetitivo enviado desde la Luna. El objetivo es decodificar las frecuencias de audio para revelar un mensaje oculto.

## Análisis y Solución

1. **Identificación de la Señal:** Al escuchar el audio, se reconoce inmediatamente el patrón de transmisión de **SSTV (Slow Scan Television)**. Este método convierte imágenes en señales de audio moduladas en frecuencia para transmitirlas por radio, una tecnología históricamente utilizada en las exploraciones espaciales.
2. **Determinación del Modo:** El audio tiene una duración aproximada de 11 minutos. En el contexto de las misiones lunares (como Apollo 11), el modo estándar empleado para codificar las imágenes era **Scottie 1** o **Martin 1**.
3. **Decodificación Forense:** 
   Para extraer la imagen sin depender de herramientas gráficas complejas, se puede utilizar la herramienta automatizada en Linux `sstv`:
```bash
   sstv -d message.wav -o flag.png
````

Al procesar el espectro de audio, el script reconstruye la matriz de píxeles original y genera una imagen limpia donde se aprecia la flag girada 180 grados.

## Bandera

 Flag: `picoCTF{beep_boop_im_in_space}`