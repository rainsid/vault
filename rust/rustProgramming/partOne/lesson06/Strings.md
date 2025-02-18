# Strings

- Rust has two kinds
	- String literals
		- text is allocated statically
		- text is immutable
	- Instances of the *String* type:
		- text is allocated on the heap
		- text is potentially mutable
		- text is deallocated at the end of the *String* object's lifetime

## Using String Literals

- you can use a string literal as follows:
``` rust
let s = "hello";
```

- Technically speaking, a string literal is a string slice with static lifetime
```rust
let s: &'static str = "hello";
```
 - A string slice knows the address of the first byte, and the number of bytes:
 ```rust
 println!("{} {:p}, {}", s, s.as_ptr(), s.len());
```


## Using the `String` Type

- you can create an instance of the `String` type as follows:
```rust
let s = String::from("hello");
```

- you can specify the variable type explicitly:
```rust
let s: String = String::from("hello");
```

- internally, a `String` object holds text as a potentially growable vector of bytes

### String memory deallocation

- at the end of the function, memory is deallocated as ff:
	- the `String` object goes out of scope, and is dropped off the stack
	- the text held by the `String` object is deallocated from the heap

- Rust defines a trait named `Drop`
	- has a `drop()` function, similar to a *destructor * in C++
	- called automatically at the end of an object's lifetime
	- allows the object to deallocated its resources

- The `String` type implements `Drop`
	- deallocates text from the heap

### Using Mutable `String` Objects

- Rust allows you to modify text in `String` object
	- Declare the `String` variable as `mut`
	- Invoke methods to modify contents
