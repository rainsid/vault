# Overview

- i a typical Rust program, you'll define many struct types
- it's common to define each struct in a separate module
	- for readability and maintainability
- example:
```rust
//Point struct ... point.rs
//Point3D struct ... point3d.rs
//Employee struct ... employee.rs
```

## Organizing your Project into Modules

- here is how
![[organize_module.png.png]]

## Defining a Struct in a Module

```rust
pub struct Point {
	pub x: i32,
	pub y: i32,
}
// mytypes/point.rs
```

- the struct type is public
	- so it's visible to other modules
- the struct fields are public
	- so they're visible to other modules

## Defining Functionality for the Struct

```rust
pub struct Point {
	pub x: i32,
	pub y: i32,
}

impl Point {
	pub fn print(&self){...}
	pub fn move_by(&mut self, dx: i32, dy: i32){...}
	fn log(&self, msg: &str){...}
}
```

- the `impl` block itself isn't public 
	- rather, we declare specific method as public, as appropriate

## Using the Struct in Client Code

- we can use the struct in client code as ff:
```rust
use crate::mytypes::point::Point;

fn some_func(){
	let mut p1 = Point {x: 10, y: 20};

	p1.move_by(100, 200);
	println!("{}", p1.to_string());
}

//other.rs
```

- we can access the `Point` type
- we can access public `Point` members