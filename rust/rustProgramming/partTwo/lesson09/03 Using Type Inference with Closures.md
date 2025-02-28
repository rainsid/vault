# Using Type Inference

- you can use type inference to simplify syntax
- omit parameter type info
	- Rust will infer the param type based on the values you pass in
- omit return type info
	- Rust will infer the return type, based on the value you returned

# Inferring the Return Type of the Closure

```rust
let get_timestamp = || Utc::now();
```
- note the simpler syntax:
	- the return type isn't specified explicitly
	- the `{}` are omitted around the closure body
- Rust infer the closure return type
	- `DateTime<Utc>` in this example

# Inferring Parameter Type of the Closure
- this closure takes a parameter (type not specified)
```rust
let reciprocal = |n| if n == 0.0 { 0.0 } else { 1.0 / n};
```
- Rust infers the type when you call the closure
```rust
println("{}", reciprocal(5.0)); // infers f64
```
- subsequent calls must use the same type:
```rust
println("{}", reciprocal(5)); //error, passes i32
```