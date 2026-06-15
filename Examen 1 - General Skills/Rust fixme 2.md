# Rust fixme 2

## Descripción

La segunda parte de la serie Rust Fixme introduce el concepto de referencias y borrowing en Rust. El código contiene errores relacionados con la mutabilidad de una cadena que se intenta modificar desde una función.

## Análisis

Al revisar `src/main.rs` encontramos la función:

```rust
fn decrypt(encrypted_buffer:Vec<u8>, borrowed_string: &String)
```

Dentro de ella se intenta modificar el contenido de `borrowed_string`:

```rust
borrowed_string.push_str("PARTY FOUL! Here is your flag: ");
```

y posteriormente:

```rust
borrowed_string.push_str(&String::from_utf8_lossy(&decrypted_buffer));
```

Sin embargo, una referencia de tipo `&String` es inmutable y no permite modificar el contenido apuntado.

## Errores Encontrados

### Error 1: Referencia inmutable

La función necesita recibir una referencia mutable.

Incorrecto:

```rust
fn decrypt(encrypted_buffer:Vec<u8>, borrowed_string: &String)
```

Correcto:

```rust
fn decrypt(encrypted_buffer:Vec<u8>, borrowed_string: &mut String)
```

### Error 2: Variable no mutable

La cadena original también debe declararse como mutable.

Incorrecto:

```rust
let party_foul = String::from("Using memory unsafe languages is a: ");
```

Correcto:

```rust
let mut party_foul = String::from("Using memory unsafe languages is a: ");
```

### Error 3: Paso de referencia mutable

La llamada a la función debe utilizar `&mut`.

Incorrecto:

```rust
decrypt(encrypted_buffer, &party_foul);
```

Correcto:

```rust
decrypt(encrypted_buffer, &mut party_foul);
```

## Concepto Aprendido

Rust diferencia entre:

```rust
&T
```

Referencia inmutable.

y

```rust
&mut T
```

Referencia mutable.

Para modificar una variable a través de una referencia, tanto la referencia como la variable original deben ser mutables.

## Ejecución

```bash
cargo run
```

Salida:

```text
Using memory unsafe languages is a: PARTY FOUL! Here is your flag: picoCTF{4r3_y0u_h4v1n5_fun_y31?}
```

## Flag

```text
picoCTF{4r3_y0u_h4v1n5_fun_y31?}
```
