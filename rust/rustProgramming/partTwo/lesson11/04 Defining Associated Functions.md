
# Overview of Associated Functions

- Rust also lets you define *associated functions*
	- similar to static methods in other OO languages
- what is an associated function?
	- a function defined in an `impl` block
	- doesn't receive a `self` parameter
	- can't access state in particular object
- associated functions define functionality that pertains to the entire struct type rather than to a particular instance

## Defining an Associated Function

```rust
pub struct Point3D {
	x: i32,
	y: i32,
	z: i32,
}

impl Poin3D {
	pub fn new(x: i32, y: i32, z: i32) -> Point3D {
		Point3D {x, y, z}	
	}
}
```

## Invoking an Associated Function 

```rust
use crate::mytypes::point3d::Point3D

fn some_func(){
	let mut p1 = Point3D::new(10, 20, 30);

	...
}
```

- note:
	- `Point3D::new()` is a factory function
	- creates a `Point3D` object on the stack
	- returns ownership to our client code