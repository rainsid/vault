# Overview

- it's common to pass structs into functions
	- it enables you to pass a lot of data into a function as a cohesive bundle
	- better than passing a myriad of individual params
- there are two ways to pass struct into a function
	- by value
	- by reference

## How to Pass a Struct Parameter by Value

- this function receives a struct param by value:
```rust 
fn consume_employee(e: Employee) {
	println!("{} {} {}", e.name, e.salary, e.fullname);
}
```

- pass in a struct by value:
```rust
fn some_higher_level_func() {
	let e1 = Employee { ... ... ... };
	consume_employee(e1);
}
```

## How Does Pass-by-Value Work for Struct Types

- if a struct implements `Copy` trait:
	- a bitwise copy of the struct is passed to the called function
	- the caller retains ownership and can use the struct afterwards
- many structs don't implement `Copy`, so:
	- ownership of the is moved to the called function
	- the caller loses ownership and can't use the struct afterwards