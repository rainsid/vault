# Overview of Closures

- closures in Rust are the equivalent of lambdas in other programming languages
- a closure is similar to a nested function, but more flexible in several respects:
	- a closure can infer parameter/return types
	- a closure can capture external variables

## Syntax for Defining a Closure

- the syntax for defining a closure is similar (but simpler) to defining a nested function:
	- define parameters inside `||`
	- optionally specify parameter/return types
	- define the closure body inside `{}`
	
- you can assign a closure to a variable
	- then use the variable as if it were a function name, to invoke the closure

---
### Defining a Closure that Takes No Params
- the closure returns a `DateTime<UTC>`
```rust
let get_timestamp = || DateTime<Utc> { Utc::now() };
```

- invocation
```rust
println!("{}", get_timestamp());
```

---
### Defining a Closure that Takes One Param
- here's a closure that takes a param of type `f64`
	- the closure also returns an `f64`
```rust
let reciprocal = |n: f64| -> f64 { if n == 0.0 {0.0} else {1.0/n} };
```

- invocation
```rust
println!("{}", reciprocal(5.0));
```

---
### Defining a Closure that Takes Many Params
- here's a closure that takes many params
	- the closure return an `i32`
```rust
let prod = |a: i32, b: i32| -> i32 { a * b };
```

- invocation
```rust
println!("{}", prod(20, 5));
```

---
### Defining a Multi-Statement Closure
- here is a closure that comprises multiple statements
	- the closure returns a `Datetime<Utc>`
	- the last expression in the closure is returned
```Rust
let get_timestamp_after_delay = 
	|seconds: u64| -> DateTime<Utc> {
		sleep(Duration::new(seconds, 0));
		Utc::now()
	};
```

- invoke
```rust
println!("{}", get_timestamp_after_delay(5));
```