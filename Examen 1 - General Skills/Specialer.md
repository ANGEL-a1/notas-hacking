## Specialer

## Descripción

Se presenta una shell restringida llamada **Specialer**, donde múltiples comandos clásicos están eliminados (como `ls`, `cat`, etc.), obligando a resolver el reto usando funcionalidades internas del shell Bash.

---

## Acceso

```bash
ssh -p 49686 ctf-player@saturn.picoctf.net
```

Password:

```text
8a707622
```

---

## Enumeración inicial

Los comandos tradicionales no funcionan:

```bash
ls → command not found
cat → command not found
```

Pero se puede usar expansión de globbing:

```bash
echo *
```

Salida:

```
abra ala sim
```

Listando estructura completa:

```bash
echo */*
```

Salida:

```
abra/cadabra.txt abra/cadaniel.txt ala/kazam.txt ala/mode.txt sim/city.txt sim/salabim.txt
```

---

## Lectura de archivos

El entorno permite **command substitution con redirección interna de Bash**:

```bash
echo "$(<archivo)"
```

Ejemplo:

```bash
echo "$(<abra/cadabra.txt)"
Nothing up my sleeve!
```

---

## Archivos importantes

```bash
abra/cadabra.txt   → Nothing up my sleeve!
abra/cadaniel.txt  → Yes, I did it! I really did it! I'm a true wizard!
ala/kazam.txt      → contiene la flag
ala/mode.txt       → pista
sim/city.txt       → UUID
sim/salabim.txt    → texto decorativo
```

---

## Obtención de la flag

```bash
echo "$(<ala/kazam.txt)"
```

Salida:

```text
return 0 picoCTF{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01ng_h3r3_49193632}
```

---

## Flag

```
picoCTF{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01ng_h3r3_49193632}
```

---

## Conceptos aprendidos

- Shell restringida

- Globbing (`*`)

- Substitución de comandos `$(<file)`

- Enumeración sin binarios básicos

- Lectura directa de archivos sin `cat`


---

## Comando clave

```bash
echo "$(<ala/kazam.txt)"
```

---

## Git (como siempre)

```bash
git add .
git commit -m "picoCTF Specialer solved - bash restricted shell bypass using file redirection"
git push
```
