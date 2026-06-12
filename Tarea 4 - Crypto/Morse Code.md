# Morse Code

## 📝 Descripción del Reto
### Enunciado:
El código morse es ampliamente conocido. El objetivo es analizar y descifrar un archivo de audio `.wav` que contiene un mensaje oculto en telegrafía.
Reglas de formato: Envolver el resultado en `picoCTF{}`, usar minúsculas y reemplazar los espacios/pausas entre palabras por guiones bajos (`_`).

---

## 🔍 Análisis de Señales y Proceso Forense

Al procesar las ondas de sonido del archivo `morse_chal.wav` mediante un decodificador adaptativo de señales, se identificaron los patrones de puntos (`.`) y rayas (`-`) correspondientes al Estándar Internacional.

### 1. Extracción de Señal Cruda (Espectrograma)
El análisis de frecuencia arrojó que la transmisión no contenía texto plano en inglés común, sino un formato de ofuscación alfanumérico clásico de internet conocido como **Leet Speak** (reemplazo visual de letras por números):

* Palabra 1: `. .-- .... ..--- --...` $\rightarrow$ `wh47`
* Palabra 2: `. .-- .... ..--- --... ....` $\rightarrow$ `h47h`
* Palabra 3: Continental Signal $\rightarrow$ `90d`
* Palabra 4: Stream Completo $\rightarrow$ `w20u9h7`

### 2. Contexto Histórico
La cadena resultante corresponde a la transcripción literal en Leet Speak de la famosa frase histórica: *"What hath God wrought"* (Qué ha forjado Dios), el primer mensaje oficial transmitido por código morse en la historia por Samuel Morse el 24 de mayo de 1844.

---

## 🏆 Flag Obtenida
**`picoCTF{wh47_h47h_90d_w20u9h7}`**