# Overview

- it is common to return a struct from a function 
	- it enables you to return a lot of data as a cohesive bundle
	- the data is useful to the calling function
- there are two ways to return a struct from a function:
	- by value
	- by reference

## How to Return a Struct by Value

```rust
fn build_employee(name: String, salary: u64, fulltime: bool) -> Employee {
	Employee {
		name: name,
		salary: salary,
		fulltime: fulltime	
	}
}
```

- this is a builder function
	- encapsulates creating a struct instance
	- returns the struct instance to the caller

### Aside: Simplifying Syntax for Initializing Fields
- the above syntax can be simplified to:

```rust
fn build_employee(name: String, salary: u64, fulltime: bool) -> Employee {
	Employee {
		name,
		salary,
		fulltime	
	}
}
```

# Receiving a Struct by Value from a Function

- we can call `build_employee()` to get back an `Employee` struct, and to own that struct
	- optionally, we can mark it as `mut`
```rust
fn some_higher_level_function(){
	let e1 = build_employee (
			String::from("Jane"),
			1000,
			true
	);


	let mut e2 = build_employee (
			String::from("Jane"),
			1000,
			false
	);

	e2.salary += 75;
	...
}
```