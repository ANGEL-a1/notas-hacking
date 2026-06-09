# More SQLi

## Descripción del Reto
Este reto de nivel medio (200 puntos) pertenece a la categoría de Explotación Web y profundiza en la explotación de Inyecciones SQL (SQLi), específicamente sobre motores de bases de datos relacionales compactos como **SQLite**. A diferencia de un bypass de autenticación simple, el objetivo requiere realizar una inyección basada en operadores de unión (`UNION-based SQLi`) para mapear el esquema de la base de datos, enumerar tablas del sistema y extraer registros confidenciales de tablas acotadas.

## Análisis de Ataques SQLi Basados en UNION
La vulnerabilidad se presenta al concatenar directamente las entradas del usuario en las consultas de búsqueda del lado del servidor. Esto permite alterar el flujo de ejecución mediante la cláusula `UNION`:
* **Operador UNION**: Permite combinar los resultados de la consulta original con los resultados de una nueva consulta inyectada por el atacante. Para que sea exitosa, ambas consultas deben poseer exactamente el mismo número de columnas y tipos de datos compatibles.
* **sqlite_master**: Es la tabla interna del sistema en entornos SQLite que almacena el esquema de la base de datos. Al consultar la columna `tbl_name` de esta tabla, un atacante puede descubrir los nombres de todas las tablas creadas en la sesión actual.

## Proceso de Reconstrucción (Enumeración y Extracción)
Para resolver el desafío, se ejecutó una metodología de explotación en tres fases:
* **Fase 1 (Bypass de Login)**: Se analizó que el servidor ordenaba los campos de validación de forma inversa (`password` primero, luego `username`). Se evadió el formulario inyectando la secuencia tautológica `' OR 1=1--` directamente en el campo de la contraseña, ganando acceso a la interfaz de búsqueda interna.
* **Fase 2 (Mapeo de Esquema)**: En el cuadro de búsqueda se determinó que la consulta original manejaba 3 columnas de salida (`City`, `Address`, `Phone`). Se inyectó el payload `' UNION SELECT tbl_name, 2, 3 FROM sqlite_master--` para listar las estructuras disponibles, identificando la tabla crítica llamada `more_table`.
* **Fase 3 (Exfiltración)**: Conociendo el nombre de la tabla objetivo, se ejecutó una consulta dirigida mediante la estructura `' UNION SELECT flag, 2, 3 FROM more_table--` para forzar la impresión del registro con el token de seguridad en la interfaz web.

## Flag Obtenida:

picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_sh0ulD_c8b7cc2a}