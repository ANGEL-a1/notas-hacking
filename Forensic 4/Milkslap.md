# Milkslap

## Descripción
El desafío proporciona una instancia de una página web con una animación interactiva (un vaso de leche siendo golpeado). El objetivo es inspeccionar los recursos del sitio, extraer la imagen base de la animación y descifrar el mensaje oculto en sus bits.

## Análisis y Solución

1. **Reconocimiento Web:** Al inicializar la instancia e inspeccionar los recursos cargados por la aplicación mediante las herramientas de desarrollador del navegador (*F12 > Network/Sources*), se detecta la carga de una imagen de fondo inusualmente larga en formato PNG, comúnmente llamada `concat_v.png`.
2. **Análisis Esteganográfico:** La imagen descargada almacena información oculta en sus capas de color. Al procesar el archivo mediante técnicas de Bit Menos Significativo (LSB), se extrae la cadena de texto plano.
3. **Automatización:** Se puede utilizar la herramienta de terminal `zsteg` en entornos Linux para escanear de forma automatizada los canales de color (`r1`, `g1`, `b1`) del PNG:
```bash
   zsteg concat_v.png
````

El comando revela inmediatamente la flag dentro del canal `b1,rgb,lsb,xy`.

## Bandera

 Flag:** `picoCTF{imag3_m4n1pul4t10n_sl4p5}`