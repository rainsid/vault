- a string slice refers to a text allocated elsewhere
- a string slice contains two pieces of info:
	- the address of a byte in the text
	- the length of the slice, in bytes
```rust
let s = "hello";
println!("{:p}, {}, {}", s.as_ptr(), s.len(), s);
```

## Understanding String Encoding in Rust
- Rust represents strings as UTF-8
	- technically, a vector of u8 bytes

- a string can contain variable-width code points
	- e.g., simple characters are 1 byte
	- e.g., complex characters might be 4 bytes

- thus Rust provides two ways to iterate over a string:
	- iterate over the raw bytes
	```rust
	let s = "hello☹";
	for b in s.bytes(){
		println!("{}", b);
	}
```
	- iterate over the characters
	```rust
	let s = "hello☹";
	for ch in s.chars(){
		println!("{}", ch);	
	}
```

## Creating a Slice as a Portion of a String

- you can create a slice as a portion of a string 
	- specify the start and end indexes (as byte positions)
	- the start index is inclusive (default is 0)
	- the end index is exclusive (default is to end of string)
```rust
let message = "hello😃";

// let s = &message[<start_index>..<end_index>]
let s = &message[1..3];
```


## Creating a Mutable String Slice
- you can define a mutable string slice
	- declare as &mut str
```rust
let mut msg = String::from("btw");
let s: &mut str = &msg;

s.make_ascii_uppercase();
```
