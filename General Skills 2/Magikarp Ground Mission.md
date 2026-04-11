# Magikarp Ground Mission

## Descripción del Reto
Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin.
Login via `ssh` as `ctf-player` with the password, `8c606eb1` on the host `wily-courier.picoctf.net` and port `50754`.

## Solución
Para resolver este reto, nos conectamos a un servidor remoto mediante SSH utilizando las credenciales proporcionadas. Una vez dentro, utilizamos comandos básicos de navegación y lectura de Linux (`cd`, `ls`, `cat`) para encontrar la bandera, la cual estaba dividida en tres partes escondidas en diferentes directorios.

Comandos utilizados en la sesión:
1. Conexión: `ssh ctf-player@wily-courier.picoctf.net -p 50754`
2. Parte 1 (Directorio inicial): `ls`, `cat 1of3.flag.txt`
3. Parte 2 (Directorio raíz): `cd /`, `ls`, `cat 2of3.flag.txt`
4. Parte 3 (Directorio home): `cd ~`, `ls`, `cat 3of3.flag.txt`

Al concatenar las tres partes obtenidas, formamos la bandera completa.

## Bandera
`picoCTF{xxsh_0ut_0f_//4t3r_0b24fc4f}`