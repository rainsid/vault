# Overview of Traits

- Traits in Rust are similar to interfaces in other OO languages

- in Rust, a trait can define:
	- abstract methods (must be overridden)
	- default methods (can be overridden)
	- constants (can be overridden)

## How to define a Trait

```rust
trait Print {
	fn print(&self);
}
```

- note: all members are implicitly `pub`
	- you can't explicitly declare as `pub`

## How to Implement a Trait

```rust
struct Employee {
	name: String,
	salary: u64,
	fulltime: bool
}

impl Employee {
	...
}

impl Print for Employee {
	fn print(&self){
		println!("{} {} {}", self.name, self.salary, self.fulltime);	
	}
}
```


## Module Organization for the Demo

- it is important to consider how to organize your code into modules
- `mytraits` module
	- defines all the traits
- `mystructs` module
	- defines all the structs that implement the traits

![[demo_module_organization.png]]

## Utilizing Trait Functionality in Client Code

- client code can utilize trait functionality 
```rust
use crate::mytraits::print::Print;
use crate::mystructs::employee::Employee;

let mut e1 = Employee::new(...);
e1.payrise(100);

e1.print();
```

- note: if you call a method defined in a trait, then you must also import that trait