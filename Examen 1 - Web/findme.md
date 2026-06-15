# findme

## Descripción

El reto proporciona una aplicación web con un formulario de login y una pista explícita:

```text
Help us test the form by submiting the username as test and password as test!
```

El objetivo es encontrar la flag analizando el comportamiento de la aplicación después de autenticarse.

---

# Reconocimiento inicial

Al acceder a la página se observa un formulario de autenticación.

Se intentó iniciar sesión con:

```text
Usuario: test
Contraseña: test
```

Sin embargo, la aplicación seguía devolviendo el mensaje inicial.

Tras revisar el reto se identificó que las credenciales correctas eran:

```text
Usuario: test
Contraseña: test!
```

---

# Análisis de tráfico HTTP

Se utilizó `curl` para inspeccionar las respuestas HTTP y seguir las redirecciones.

```powershell
curl.exe -v -L -d "username=test&password=test!" http://saturn.picoctf.net:55908/login
```

---

# Primera redirección

La respuesta del servidor fue:

```http
HTTP/1.1 302 Found
Location: /next-page/id=cGljb0NURntwcm94aWVzX2Fs
```

Se identificó un valor Base64 en el parámetro `id`.

Valor:

```text
cGljb0NURntwcm94aWVzX2Fs
```

Decodificación:

```text
picoCTF{proxies_al
```

---

# Segunda redirección

Al seguir la URL, el servidor devolvió una página HTML con JavaScript:

```html
<script>
window.location="/next-page/id=bF90aGVfd2F5X2JlNzE2ZDhlfQ==";
</script>
```

Se observó un segundo fragmento codificado en Base64.

Valor:

```text
bF90aGVfd2F5X2JlNzE2ZDhlfQ==
```

Decodificación:

```text
l_the_way_be716d8e}
```

---

# Reconstrucción de la flag

Primer fragmento:

```text
picoCTF{proxies_al
```

Segundo fragmento:

```text
l_the_way_be716d8e}
```

# Flag

```text
picoCTF{proxies_all_the_way_be716d8e}
```
