# Copying vs Moving

## `Copy` Trait
- Rust defines a trait names `Copy`
	- indicates variables can be duplicated by copying bits
- simple types (e.g. `i8`) implement `Copy`
	- the value of `b` is *bit-copied* into `a`
- Most types (example is `String`) don't implement `Copy`
	- the value of `b` is *moved* into `a`
	- the variable `b` can't be used thereafter

### Copying a value
```rust
let a  = 42;
let b = a;

println!("{}, {}", a, b); // 42, 42
```

- `=` copies the value from `a` to `b`
- you can use `a` afterwards

### Moving a value
```rust
let s1 = String::from("hello");
let s2 = s1;

println!("{}", s2); // "hello"
println!("{}", s1); // compiler error
```

- `=` moves the value (which is a pointer value) from `s1` into `s2`
- you can't use `s1` afterwards