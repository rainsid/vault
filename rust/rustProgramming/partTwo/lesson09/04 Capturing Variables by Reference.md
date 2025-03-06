# How Capturing Works

- the Rust compiler decides how to capture a variable:
	- capture an immutable reference
	- capture a mutable reference
	- capture the value(move ownership)

## Capturing an Immutable Reference

```rust
fn capture_immutable_reference() {
	let b1 = String::from("|-------------------------------------|");
	let b2 = String::from("|-------------------------------------|");

	let display_heading = |s| {
		println!("{}", b1);
		println!("| {:<15} |", s);
		println!("{}", b2);
	}

	display_heading(String::from("hello"));
	display_heading(String::from("goodbye"));

	println!("{} {}", b1, b2); 
}
```

## Capturing a Mutable Reference
```rust
fn capture_mutable_reference(){
	let mut b1 = String::from("|-------------------------------------|");
	let mut b2 = String::from("|-------------------------------------|");
	
	let mut display_heading = |s| {
		b1.push_str("x");
		b2.push_str("x");
		println!("{}", b1);
		println!("| {:<15} |", s);
		println!("{}", b2);
	}

	display_heading(String::from("hello"));
	display_heading(String::from("goodbye"));

	println!("{} {}", b1, b2);
}
```