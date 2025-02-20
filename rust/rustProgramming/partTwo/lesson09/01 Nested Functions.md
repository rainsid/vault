# Defining a Nested Function

- you can define a nested function
	- i.e., a function nested inside an outer function
	- only visible within the outer function
```rust
fn some_outer_function {
	fn sqr(i: i32) -> i32 {
		i * i
	}

	println!("Square of 5 is {}", sqr(5));
	println!("Square of 7 is {}", sqr(7));
}
```

# Fun Facts About Nested Functions

- you must specify full type info for a nested function
	- parameter types / return type
	
- a nested function cannot access variables in the outer scope
	- you must pass any values you need as parameters into the function
