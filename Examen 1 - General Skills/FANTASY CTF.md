### Descripción del Reto

Este reto es una ficción interactiva basada en texto que simula la participación de una estudiante llamada Eibhilin en la edición del año 3025 de picoCTF. El objetivo principal del ejercicio es familiarizar al usuario con las conexiones remotas por medio de `netcat` (`nc`) y repasar las **reglas de juego limpio e integridad (Rules & Scope)** de la plataforma.

### Conceptos Clave y Reglas de la Competencia

A través de la simulación del asistente de IA `Nyx`, el reto evalúa y refuerza cuatro reglas de comportamiento ético indispensables en cualquier CTF:

1. **Registro único:** Cada participante debe competir utilizando única y exclusivamente **una sola cuenta** individual. Crear cuentas espejo o duplicadas es motivo de descalificación inmediata.

2. **No compartir recursos:** Está estrictamente prohibido compartir accesos a cuentas de usuario, flags obtenidas o archivos descargables (_artifacts_) con otros competidores ajenos a tu equipo oficial.

3. **Políticas de Writeups:** Documentar soluciones e ideas es excelente para el aprendizaje, pero los writeups **no deben publicarse de manera abierta/pública** en internet sino hasta que la competencia haya concluido formalmente y los organizadores anuncien a los ganadores.


### Resolución del Reto (Paso a Paso)

#### 1. Conexión Remota

El reto requiere interactuar con un servicio expuesto en un puerto específico. Para establecer el puente de comunicación en la Webshell, se ejecuta el comando `netcat`:


```
nc verbal-sleep.picoctf.net 61496
```

#### 2. Toma de Decisiones en la Simulación

- **Pregunta 1 (Método de registro):** Se selecciona la opción **`c`** (_Register a single, private account_) para cumplir con el registro individual regulado.

- **Pregunta 2 (Búsqueda de Flags):** Se selecciona la opción **`a`** (_Play the game_) para jugar el reto legítimamente en lugar de intentar buscar soluciones o filtraciones en la red.


Al cumplir con el flujo de decisiones éticas, la simulación concluye con éxito liberando el token en texto plano.

###  Flag 

```
picoCTF{m1113n1um_3d1710n_1e2b417a}
```