# Chrono

## Descripción del Reto

Este reto de nivel medio (100 puntos) aborda la automatización y planificación de tareas a intervalos regulares dentro de sistemas operativos Linux. El objetivo es identificar cómo y dónde se configuran estos intervalos de ejecución en un servidor de producción y auditar el archivo correspondiente para extraer la bandera (flag).

## Análisis de Planificación de Tareas (Cron)

En entornos Unix/Linux, el demonio encargado de la ejecución programada de tareas en segundo plano es **cron**. Toda la configuración de estas tareas automatizadas se almacena en archivos específicos del sistema:

- `/etc/crontab`: Archivo principal de configuración del sistema que define las variables de entorno de cron y la tabla de planificación general (minuto, hora, día del mes, mes, día de la semana, usuario y comando).
    
- `/etc/cron.d/`: Directorio modular donde paquetes y servicios del sistema instalan sus propios archivos de planificación de tareas utilizando la misma sintaxis que `/etc/crontab`.
    

## Proceso de Reconstrucción (Inspección de Tareas Programadas)

Para resolver el desafío, se auditó el entorno del servidor remoto estableciendo una conexión de consola interactiva:

- Se estableció una sesión segura mediante SSH con las credenciales asignadas al reto: `ssh -p 59066 picoplayer@saturn.picoctf.net`.
    
- Se descartó la inspección de archivos individuales del directorio personal y el uso del comando local `crontab -l` debido a que la automatización analizada pertenece a configuraciones globales del sistema.
    
- Se leyó de forma directa el archivo central de tareas programadas utilizando el comando `cat /etc/crontab`.
    
- Se identificó que la bitácora de tareas programadas del sistema operativo contenía un registro donde se definía la bandera del reto de manera explícita.
    

## Flag Obtenida:

picoCTF{Sch3DUL7NG_T45K3_L1NUX_d83baed1}