- using return statement:
```rust
fn some_func(params...) -> some_type {
	return some_value_of_that_type;
}
```

- if the function ends with an expression, the expression is the return value
```rust
fn some_func(params...) -> some_type {
	some_value_of_that_type
}
```

# Returning a Copyable Value

- when you return a copyable value(e.g. `i32`):
	- Rust bit-copies the value back to the caller
```rust
fn some_higher_level_func() {
	let n = f1(); // recieves a copy
	println!("{}", n);
}

fn f1() -> i32 {
	let n = 42;
	return n; // returns a copy
}
```

# Returning a Non-Copyable Value

- when you return a non-copyable value (e.g., `String`)
	- Rust moves ownership of the value back to the caller
	- the caller now owns the value
```rust
fn some_higher_level_func() {
	let s = f2();
	println!("{}", s);
}

fn f2 -> String {
	let s = String::from("hello");
	return s;
}
```