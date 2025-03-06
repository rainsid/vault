# Capturing Variables by Value

- a closure can capture a variable by value
	- necessary if the closure requires
- when a closure captures a variable by value:
	- Rust moves ownership of the variable into the closure
- after the closure body:
	- the outer function loses ownership of the variable and can't use it

# Capturing Variables by Value Automatically

- this closure captures by value automatically:
```rust
let message = String::from("hello");
...
let consume_message = || {
	println!("Message in closure: {}", message);
	std::mem::drop(message);
};

//can't use `message` here, it's owned by closure
```

- the closure calls `std::mem::drop()`, which requires ownership of `message`

# Capturing Variables by Value Forcibly

- you can force a closure to capture variables by value 
	- prefix the closure with the `move` keyword

- this is useful when you spawn another thread
	- the thread executes the code in closure
	- the thread might outlive the outer function
	- so the closure must capture variables by value
```rust
let message = String::from("HELLO");

std::thread::spawn(move || {
	println!("Message initiallly: {}", message);
	std::thread::sleep(Duration::new(5,0));
	println!("Message afterward: {}", message);
})
```