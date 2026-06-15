## Python Wrangling

## Descripción del Reto

Este reto de nivel medio (10 puntos) pertenece a la categoría **General Skills** y está enfocado en comprender cómo ejecutar scripts de Python desde la terminal y analizar su funcionamiento para recuperar información cifrada.

El objetivo consiste en utilizar un script proporcionado (`ende.py`) junto con una contraseña almacenada en `password.txt` para descifrar el contenido de un archivo cifrado (`flag.txt.en`) y obtener la bandera.

---

## Archivos Proporcionados

El reto incluye los siguientes archivos:

```text
ende.py
password.txt
flag.txt.en
```

Contenido de la contraseña:

```text
720b6ad346f84cd483c60c7464dd95d4
```

---

## Análisis del Script

Al revisar el código fuente se observa que el programa admite dos modos de operación:

```bash
python ende.py -e archivo
```

Para cifrar archivos.

```bash
python ende.py -d archivo
```

Para descifrar archivos.

La sección relevante del código es:

```python
ssb_b64 = base64.b64encode(sim_sala_bim.encode())
c = Fernet(ssb_b64)
```

Aquí el programa:

1. Toma la contraseña proporcionada.
    
2. La convierte a Base64.
    
3. Utiliza el resultado como clave para el algoritmo Fernet.
    
4. Descifra el contenido del archivo indicado.
    

---

## Identificación de la Solución

En lugar de intentar romper el cifrado, el reto proporciona directamente la contraseña necesaria en:

```text
password.txt
```

Por lo tanto únicamente es necesario utilizar el modo de descifrado del script.

---

## Ejecución

Se ejecuta el programa utilizando:

```bash
python ende.py -d flag.txt.en 720b6ad346f84cd483c60c7464dd95d4
```

Donde:

- `-d` indica modo descifrado.
    
- `flag.txt.en` es el archivo cifrado.
    
- `720b6ad346f84cd483c60c7464dd95d4` es la contraseña obtenida de `password.txt`.
    

El programa procesa el archivo utilizando Fernet y muestra el contenido original.

---

## Flag Obtenida

```text
picoCTF{4p0110_1n_7h3_h0us3_9c5f9bcf}
```
