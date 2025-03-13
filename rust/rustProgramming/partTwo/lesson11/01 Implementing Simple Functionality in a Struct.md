# Defining Functionality for a Struct

- it's also possible to define functionality for a struct:
```rust
struct Point {
	x: i32,
	y: i32
}

impl Point {
	//define methods for the Point Struct
}
```

- this is similar to defining methods in a class in other Object Oriented languages

## How to Define a Method

- to define a method for a struct:
	- define a function inside the `impl` block
- the first param must be named `self`
	- it must be a reference to a struct instance
	- the method borrows the instance
- inside the method:
	- the `self ` to access struct fields

### Defining Methods

```rust
impl Point {
	fn print(self: &Point) {
		println!("{}, {}", self.x, self.y);
	}
}
```

- you can use `Self` as a type alias:
```rust
fn print(self: &Self){
	...
}
```

- you can also use shorthand syntax:
```rust
fn print(&self){
	...
}
```

## Invoking Methods

- to invoke a method:
	- use the syntax `anInstance.aMethod(params)` 
```rust
let p1 = Point {x:10, y: 20};

p1.print();
```

- Rust passes the instance into the `self` param in the method