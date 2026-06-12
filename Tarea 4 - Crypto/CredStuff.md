# CredStuff

## 📝 Descripción del Reto

### Ennciado:
Se interceptó una filtración de credenciales de inicio de sesión de un sitio web del mercado negro. El objetivo es encontrar la contraseña del usuario `cultiris` dentro del volcado y descifrarla con éxito.

---

## 🔍 Análisis Forense y Criptográfico

El archivo comprimido `leak.tar` contiene una estructura con dos archivos de texto principales:
1. `usernames.txt`: Lista masiva de nombres de usuario legítimos.
2. `passwords.txt`: Lista de contraseñas asociadas uno a uno en el mismo orden de línea que los usuarios.

### 1. Localización del Objetivo
Utilizando herramientas de búsqueda de texto (o automatización en Python), se procedió a localizar la línea exacta del usuario objetivo `cultiris` dentro de `usernames.txt`. El usuario fue hallado específicamente en la **línea 378** del archivo.

### 2. Extracción del Payload Cifrado
Al inspeccionar la **línea 378** del archivo `passwords.txt`, se recuperó la contraseña asociada, la cual presentaba una estructura de ofuscación evidente:

`cvpbPGS{P7e1S_54I35_71Z3}`

### 3. Identificación del Cifrado
La firma del string mantiene un patrón idéntico al formato estándar de las banderas de la plataforma (`picoCTF{...}`). Al analizar la distancia de los caracteres, se determinó el uso del algoritmo **ROT13** (Cifrado César con un desplazamiento de $13$ posiciones en el alfabeto).

---

## 🛠️ Solución y Automatización (Python)

Se implementó un script local en Python utilizando la librería nativa `codecs` para procesar el flujo y realizar el desplazamiento simétrico de los caracteres de forma automatizada:

```python
import codecs

# Cadena cifrada extraída de la línea 378
password_cifrado = "cvpbPGS{P7e1S_54I35_71Z3}"

# Decodificación criptográfica usando el esquema ROT13
flag_descifrada = codecs.decode(password_cifrado, 'rot_13')

print(f"Flag Recuperada: {flag_descifrada}")
````

### 🔓 Traducción del texto:

- `cvpbPGS` → `picoCTF`
    
- `P7e1S_54I35_71Z3` → `C7r1F_54V35_71M3`
    

## 🏆 Flag Obtenida

**`picoCTF{C7r1F_54V35_71M3}`**