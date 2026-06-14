# Operation Orchid

## Descripción
El desafío proporciona una imagen de disco comprimida (`disk.flag.img.gz`). El objetivo es analizar el sistema de archivos de la imagen, investigar los rastros de actividad del usuario y descifrar el archivo que contiene la bandera.

## Análisis y Solución

1. **Montaje y Exploración de la Imagen:**
   Al descomprimir y explorar la imagen de disco con herramientas de análisis forense (como `Sleuth Kit` / `fls` o montándola directamente en Linux), se identifica una estructura de archivos basada en una distribución ligera (Alpine Linux).
   
2. **Análisis de Rastros (History Carving):**
   Al revisar el directorio raíz del usuario (`/root`), se localiza el archivo oculto `.ash_history`, el cual registra los últimos comandos ejecutados en la terminal. El historial revela la siguiente línea crítica:

   openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
   
Esto demuestra que el archivo original `flag.txt` fue eliminado tras ser cifrado con el algoritmo **AES-256** bajo la contraseña maestra `unbreakablepassword1234567`.

3. **Descifrado del Artefacto:** Extrayendo el archivo cifrado `flag.txt.enc` del sistema de archivos, se procede a revertir el comando utilizando OpenSSL con la clave recuperada:


   openssl aes256 -d -salt -in flag.txt.enc -out flag.txt -k unbreakablepassword1234567


Al ejecutar el descifrado, el archivo `flag.txt` vuelve a su estado original en texto plano, exponiendo la bandera legítima.


## Bandera

**🏆 Flag:** `picoCTF{h4un71ng_p457_0a710765}`