# SQL Direct
Descripción del Problema
El reto consiste en auditar y explorar un servidor de bases de datos PostgreSQL remoto provisto por la plataforma de picoCTF. Se nos otorga acceso directo como el superusuario administrativo (`postgres`), teniendo como objetivo inspeccionar la estructura interna del sistema, listar las tablas del esquema público y extraer la bandera oculta dentro de los registros.

# Análisis y Solución

## Fase 1: Identificación del Entorno Local y Conectividad

Al intentar interactuar de forma nativa con el comando clásico de conexión (`psql`), la terminal local de Windows devuelve un error de comando no encontrado (`CommandNotFoundException`). Adicionalmente, el entorno local de Python se encuentra bajo una política de entorno administrado de forma externa por el gestor `uv` (PEP 668), lo que bloquea las instalaciones directas y globales de paquetes mediante `pip`.

## Fase 2: Evasión de Restricciones mediante Scripting Aislado

Para evadir la falta de un cliente nativo y sortear las restricciones del sistema administrado sin alterar el entorno global, se opta por instalar de manera forzada el conector binario aislado de PostgreSQL (`psycopg2-binary`) utilizando la bandera `--break-system-packages`.

Posteriormente, se desarrolla un script automatizado para interactuar de forma programática con la base de datos a través del puerto activo de la instancia (`56479`), el cual realiza las siguientes acciones:

Listar Directorio e Inspección:

Payload:

```
import psycopg2

try:
    conn = psycopg2.connect(
        user="postgres", password="postgres",
        host="saturn.picoctf.net", port="56479", database="pico"
    )
    cur = conn.cursor()
    cur.execute("SELECT table_name FROM information_schema.tables WHERE table_schema = 'public';")
    tables = cur.fetchall()
    
    if tables:
        tabla_objetivo = tables[0][0]
        cur.execute(f"SELECT * FROM {tabla_objetivo};")
        for fila in cur.fetchall():
            print(f"Resultado: {fila}")
finally:
    if 'conn' in locals() and conn:
        cur.close() ; conn.close()
```

# Flag

picoCTF{L3arN_S0m3_5qL_t0d4Y_21c94904}