# Introduction to Structs in Rust

- Rust allows you to define structure types (*structs*)
- a struct can contain:
	- related fields
	- related functionality
	- trait implementations
- structs in Rust are quite similar to classes in other languages

## How to Define a Struct Type

- to define a struct type:
	- use the `struct` keyword
	- give the struct a name, starting with a capital
	- define field names and types

```rust
struct Employee {
	name: String,
	salary: f64,
	fulltime: bool
}
```

## Struct Visibility
- by default, a struct and its fields are private
	- only visible in the module in which they are defined
	
- if you want a struct to be visible in other modules:
	- declare the struct as `pub`

## Organizing your Code into Modules

- define a struct type in a separate module file, with public visibility of the struct and its fields
```rust
pub struct Employee {
	pub name: String,
	pub salary: u64, 
	pub fulltime: bool
} // mytype.rs
```

- you can declare the module to your crate as follows:
```rust
mod mytypes;

// main.rs
```

## Using a Struct Type
- to use struct type in your program code, you can use its fully-qualified name
```rust
let e1 : crate::mytypes::Employee;  //other.rs
```

- or you can import its name
```rust
use crate::mytypes::Employee;
...

let e2: Employee;   
//others.rs
```








































