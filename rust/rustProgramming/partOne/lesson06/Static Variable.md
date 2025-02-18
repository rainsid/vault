# Static variable
- to define
	- use `static` keyword
	- specify the variable name, in caps
	- specify the data type
	- supply a value, typically a constant
``` rust
fn some_func(){
	static MESSAGE: &str = "Hello";
}
```

---
## Initializing a Static Variable Lazily
- Imagine you want to initialize a static variable lazily
	- i.e., provide an initial value that is computed at run-time
- This simple approach won't work
```rust
fn some_func(){
	static TIMESTAMP: DateTime<Utc> = Utc::now();
}
```

- this code is not thread safe
	- multiple threads might access the static variable at the same time

---
- To initialize a static variable safely at run time:
	- use the `Lazy<T>` type
```rust
fn some_func(){
	static TIMESTAMP: Lazy<DateTime<Utc>> = Lazy::new(|| Utc::now()); // `|| Utc::now()` is called a closure

	println!("{}", *TIMESTAMP);
}
```

- the *Lazy* object wraps a value safely 
	- the value is initialized on first access
	- access to the value is thread-safe