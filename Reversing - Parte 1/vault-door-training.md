### Descripción del Reto

Este reto sirve como introducción práctica a la serie de bovedas (`vault-doors`) dentro de la categoría de Ingeniería Inversa. Su objetivo principal es familiarizarse con la estructura de los retos en Java, comprender el funcionamiento del envoltorio de la bandera (`picoCTF{...}`) y observar cómo se realiza una comprobación de contraseña sin técnicas de ofuscación de código.

### Análisis del Código Fuente

Al abrir el archivo `VaultDoorTraining.java`, se observa que el programa captura la entrada del usuario (`userInput`) y limpia el formato eliminando los caracteres externos correspondientes a `picoCTF{}`.

Posteriormente, invoca al método de validación `checkPassword(String password)`. A diferencia de los niveles posteriores que usan operaciones a nivel de bits, matrices o codificaciones complejas, el Minion #9567 dejó la contraseña quemada directamente en texto plano (`hardcoded`) usando la función nativa `.equals()`:

Java

```
public boolean checkPassword(String password) {
    return password.equals("w4rm1ng_Up_w1tH_jAv4_000HPpgh7Ph");
}
```

Al estar expuesta de manera directa en el código fuente, no es necesario realizar ningún proceso de de-ofuscación o script inverso.

**Flag Obtenida:** `picoCTF{w4rm1ng_Up_w1tH_jAv4_000HPpgh7Ph}`