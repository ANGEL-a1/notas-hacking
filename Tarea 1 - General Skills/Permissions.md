# Permissions

## Descripción del Reto

Este reto de nivel medio (100 puntos) aborda la gestión de privilegios y el control de accesos basados en roles dentro de sistemas operativos Linux. El objetivo es ingresar a un entorno restringido con un usuario de bajos privilegios (`picoplayer`), auditar las políticas de elevación de seguridad configuradas por el administrador del sistema y encontrar una vía para leer un archivo restringido ubicado en el directorio raíz del superusuario (`/root`).

## Análisis de Permisos y Elevación (Sudoers)

En entornos Unix/Linux, la separación de privilegios impide que usuarios estándar interactúen con archivos críticos del sistema operativo. Para auditar y evadir estas restricciones de forma legítima, se analizan los siguientes componentes:

- `sudo -l`: Comando que interroga al archivo de configuración `/etc/sudoers` para listar los comandos específicos que el usuario actual tiene permitido ejecutar con los privilegios de cualquier otro usuario (incluyendo `root`) de manera explícita sin requerir la clave de administrador.
    
- **Explotación de Vi (GTFOBins)**: El editor de texto clásico `vi` posee una función integrada de escape sintáctico mediante el operador `!`. Si el binario es ejecutado con permisos elevados a través de `sudo`, invocar un cascarón secundario (`:!sh`) hereda de forma automática el contexto de seguridad de `root`.
    

## Proceso de Reconstrucción (Escalación de Privilegios)

Para resolver el desafío, se interactuó con el servidor remoto a través de una sesión de terminal para identificar fallas en la asignación de permisos:

- Se estableció una sesión segura mediante SSH utilizando las credenciales provistas: `ssh -p 52625 picoplayer@saturn.picoctf.net`.
    
- Se ejecutó el comando `sudo -l` para evaluar qué binarios o herramientas del sistema contaban con políticas de ejecución preferenciales para nuestra cuenta, detectando la regla explícica `(ALL) /usr/bin/vi`.
    
- Se inicializó el editor de texto con privilegios de superusuario ejecutando el comando `sudo /usr/bin/vi`.
    
- Desde la interfaz interactiva de Vim, se introdujo la secuencia de comandos `:!sh` para romper el entorno del editor y desplegar una consola interactiva de root (`#`).
    
- Se listó el directorio del superusuario y se leyó el archivo oculto correspondiente utilizando el comando `cat /root/.flag.txt` para extraer la estructura explícita de la bandera.
    

## Flag Obtenida:

picoCTF{uS1ng_v1m_3dit0r_f6ad392b}