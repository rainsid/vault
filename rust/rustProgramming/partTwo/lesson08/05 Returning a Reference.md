```rust
fn some_func(params...) -> &some_type {
	return &some_value_of_that_type
}
```


# How to Use a Returned Reference

- imagine you call a function that returns a reference, and you wan to assign the result to a var...
- you can use implicit typing:
```rust
fn some_higher_level_func(){
	let r = some_func();
}
```

- or you can use explicit typing:
```rust
let r: &some_type = some_func();
```


## Lifetime Management

- Rust doesn't allow you to return a dangling reference 
	- you can't return a reference to a a local stack-based object
```rust
// !!!!! these functions causes an error

fn bad_func1() -> &String {
	let s = String::from("hello");
	&s // error! Returns ref to local s
}

fn bad_func2() -> &String {
	&s // error! Returns ref to local s
}
```


## Lifetime Management

- here's a common way to ensure the lifetime of an object:
	- pass an obj by reference into a function
	- in the function, return a reference to the same object
```rust
fn some_high_level_func() {
	let s = String::from("hi");
	let r = good_func(&s);
	println!("{}", r);
}

fn good_func(s: &String) -> &String {
	...  // use s
	s    // return s (which is a ref)
}
```

## Returning a String Literal

- imagine a function that tries to return a string literal:
```rust
fn some_func() -> &str {
	//return a string literal
}

//this does not compile 
//lifetime of borrowed object is not known
```

- to fix the problem, you can provide a `static` lifetime parameter:
```rust
fn some_func() -> &'static str {
	// return a stirng literal
}
```









































































































