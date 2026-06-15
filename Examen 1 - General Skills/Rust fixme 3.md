# Rust fixme 3

## Descripción

Tercera parte de la serie Rust Fixme. El código contiene un error relacionado con operaciones inseguras (unsafe) en Rust.

## Análisis

Al ejecutar:

```bash
cargo run
```

Rust devuelve un error similar a:

```text
error[E0133]: call to unsafe function `std::slice::from_raw_parts` is unsafe and requires unsafe function or block
```

La función:

```rust
std::slice::from_raw_parts(...)
```

es considerada unsafe porque trabaja directamente con punteros crudos (raw pointers).

## Código Problemático

```rust
// unsafe {
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);

    let decrypted_ptr = decrypted_buffer.as_ptr();
    let decrypted_len = decrypted_buffer.len();

    let decrypted_slice =
        std::slice::from_raw_parts(
            decrypted_ptr,
            decrypted_len
        );

    borrowed_string.push_str(
        &String::from_utf8_lossy(decrypted_slice)
    );
// }
```

Los comentarios del propio código indican la solución:

```rust
// unsafe {
...
// }
```

## Solución

Descomentar el bloque:

```rust
unsafe {
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);

    let decrypted_ptr = decrypted_buffer.as_ptr();
    let decrypted_len = decrypted_buffer.len();

    let decrypted_slice =
        std::slice::from_raw_parts(
            decrypted_ptr,
            decrypted_len
        );

    borrowed_string.push_str(
        &String::from_utf8_lossy(decrypted_slice)
    );
}
```

## Conceptos Aprendidos

### Safe Rust

Rust normalmente impide:

- Dereferenciar punteros crudos.
    
- Acceder a memoria inválida.
    
- Crear referencias inconsistentes.
    

### Unsafe Rust

Con:

```rust
unsafe {
    ...
}
```

el programador asume la responsabilidad de garantizar que la operación sea segura.

## Ejecución

```bash
cargo run
```

Salida:

```text
Using memory unsafe languages is a: PARTY FOUL! Here is your flag: picoCTF{n0w_y0uv3_f1x3d_1h3m_411}
```

## Flag

```text
picoCTF{n0w_y0uv3_f1x3d_1h3m_411}
```
