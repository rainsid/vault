```rust
struct Rectangle {
	width: u32,
	height: u32,
}
fn main(){
	let rect1 = Rectangle {
		width: 30,
		height: 50,	
	};

	println!("The are of the rectangle is  {} square pixels", area(&rect1));
}

fn area(rect: &Rectangle) -> u32 {
	rect.width * rect.height
}
```
- we use structs to add meaning by labeling the data


 ## Adding Useful Functionality with Derived Traits
 
- Rust *does* include functionality  to print out debugging info, but we have to explicitly opt in to make that functionality available for out struct
- we add the outer attribute `#[derive(Debug)]`
```rust
#[derive(Debug)]
struct Rectangle {
	width: u32,
	height: u32,
}

fn main() {
	let rect1 = Rectangle {
		width: 30,
		height: 50,	
	};
println!("rect1 is {rect:?}");
}
```
- in cases when we want to have output that is a bit easier to read, we can use `{:#?}`
```rust
println!("rect is {rect:#?});
```

- another way is using the `dbg!` macro, which takes ownership of an expression
```rust
#[derive(Debug)]
struct Rectangle {
	width: u32,
	height: u32,
}

fn main() {
	let scale = 2;
	let rect1 = Rectangle {
		width: dbg!(30 * scale),
		height: 50,	
	};
dbg!(&rect1);
}
```
