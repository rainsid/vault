- Memory management in Rust is different to most other languages

---
# Defining a Variable with Local Scope
- When you  define a variable in a function:
	- the variable has local scope
```rust
fn some_func(){
	let x = 42;
} //x goes out scope here
```

	- the variable goes out of scope at the closing `}`
```rust
fn some_func(){
	if some_test {
		let s1 = "JonSnow";
		println!("{}", s1);
	}
	//s1 can't be accessed here
}
```

## Where is memory allocated
- when you declare a variable anywhere in a function:
	- it is allocated on the stack, by default
	- it is popped off the stack at the end of the function
- it's also possible to allocate memory elsewhere in Rust
	-  static storage
	- heap-base storage




























