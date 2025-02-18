- *Methods* are similar to functions: we declare them with the `fn` keyword and a name, they can have parameters and a return value

## Defining Methods
```rust
#[derive(Debug)]
struct Rectangle {
	width: u32,
	height: u32,
}

impl Rectangle {
	fn area(&self) -> u32 {
		self.width * self.height	
	}
}

fn main() {
	let rect1 = Rectangle {
		width: 30, 
		height: 50,
	};

	println!(
		"The area of the rectangle is {} square pixels.", rect1.area()
	);
}
```

- the `impl` (implementation) block is associated with the `Rectangle` type
- the function `area` within the `impl` is called a *method* 
- the `&self` is short for `self: &Self` where `Self` is an alias for the type that the `impl` block is for
- main reason for using methods instead of functions, is for organization

```rust
impl Rectangle {
	fn width(&self) -> bool {
		self.width >  0	
	}
}

fn main() {
	let rect1 = Rectangle {
		width: 30, 
		height: 50,	
	};

	if rect1.width() {
		println!("The rectangle has a nonzero width; it is {}", rect1.width);
	}
}
```
- we can choose to give a method the same name as on of the struct's fields
- often, when we give a method name the same name as a field we want it to only return the value in the field and do nothing else, method like this is called *getter*

## Methods with More Parameters

```rust

struct Recatangle {
	width: u32,
	height: u32,
}
impl Rectangle {
	fn area(&self) -> u32 {
		self.width * self.height	
	}

	fn can_hold(&self, other: &Rectangle) -> {
		self.width > other.width && self.height > other.height	
	}
}

fn main() {
	let rect1 = Rectangle {
		width: 30, 
		height: 50,	
	};
	let rect2 = Rectangle {
		width: 10, 
		height: 40,	
	};
	let rect3 = Rectangle {
		width: 60, 
		height: 45,	
	};

	println!("Can rect1 hold rect2?  {}", rect1.can_hold(&rect2));
	println!("Can rect1 hold rect3?  {}", rect1.can_hold(&rect3));
	
}
```

## Associated Functions

- all functions defined within an `impl` block are called *associated functions* 
- functions that don't have `self` as their first param are not methods
	- they don't need an instance of the type to work with
- associated functions that aren't methods are often used for constructor that will return a new instance of the struct
```rust
impl Rectangle {
	fn square(size: u32) -> Self {
		Self {
			width: size,
			height: size	
		}	
	}
}
```
- in the example, an associated function named `square` has one dimension param to be used as both width and height, making it easier to create a square `Rectangle` rather than specifying the same value twice
- the `Self` keywords (return type and in the body of the function) are aliases for the type that appears after the `impl`
- to call this associated function, we use the `::` syntax with the struct name
```rust
let sq = Rectangle::square(3);
```
- this function is namespaced by the struct

## Multiple `impl` Blocks

- each struct is allowed to have multiple `impl` blocks
- there is no reason to separate these methods but this is valid
```rust
impl Rectangle {
	fn area(&self) -> u32 {
		self.width * self.height	
	}
}

impl Rectangle {
	fn can_hold(&self, other: &Rectangle) -> Bool {
		self.width > other.width && self.height > self.height	
	}
}
```