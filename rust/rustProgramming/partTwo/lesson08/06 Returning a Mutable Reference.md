# How to Return a Mutable Reference
- here is how to return a mutable ref:
```rust
fn some_func(params...) -> &mut some_type {
	...
	return &mut some_value_of_that_type;
}
```

- do's and don'ts:
	- do comply with the borrow checker
	- don't return a dangling reference

# How to Use a Returned Mutable Reference

- you can use implicit typing
```rust
fn some_higher_level_func(){
	let r = some_func();
}
```

- or you can use explicit typing:
```rust
fn some_higher_level_func(){
	let r: &mut some_type = some_func();
}
```
