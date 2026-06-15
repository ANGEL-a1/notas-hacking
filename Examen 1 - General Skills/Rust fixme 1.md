# Rust fixme 1

## Descripción

Se proporciona un proyecto en Rust con errores de sintaxis. El objetivo es corregir dichos errores para que el programa compile correctamente e imprima la flag.

## Análisis

Al revisar el archivo `src/main.rs`, se observan comentarios que indican posibles errores de sintaxis:

```rust
let key = String::from("CSUCKS"); // How do we end statements in Rust?
```

```rust
return; // How do we return in rust?
```

```rust
println!(
    "{}",
    String::from_utf8_lossy(&decrypted_buffer)
);
```

El programa utiliza la librería `xor_cryptor` para descifrar un arreglo de bytes codificados en hexadecimal mediante una clave XOR.

### Fragmento relevante

```rust
use xor_cryptor::XORCryptor;

fn main() {
    let key = String::from("CSUCKS");

    let hex_values = [
        "41", "30", "20", "63", "4a", "45", "54", "76",
        "01", "1c", "7e", "59", "63", "e1", "61", "25",
        "7f", "5a", "60", "50", "11", "38", "1f", "3a",
        "60", "e9", "62", "20", "0c", "e6", "50", "d3",
        "35"
    ];

    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let res = XORCryptor::new(&key);

    if res.is_err() {
        return;
    }

    let xrc = res.unwrap();

    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);

    println!(
        "{}",
        String::from_utf8_lossy(&decrypted_buffer)
    );
}
```

## Problemas Encontrados

### Error 1: Finalización de sentencia

Rust requiere punto y coma (`;`) para finalizar instrucciones.

Correcto:

```rust
let key = String::from("CSUCKS");
```

### Error 2: Retorno

La función debe utilizar la palabra reservada `return`.

Correcto:

```rust
return;
```

### Error 3: Impresión de variables

Para imprimir una variable con `println!` se utiliza el especificador `{}`.

Correcto:

```rust
println!("{}", variable);
```

## Ejecución

Una vez corregidos los errores:

```bash
cargo run
```

El programa compila y ejecuta el proceso de descifrado XOR.

## Flag

```text
picoCTF{4r3_y0u_4_ru$t4c30n_n0w?}
```
