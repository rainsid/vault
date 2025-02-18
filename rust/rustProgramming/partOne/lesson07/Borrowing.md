# Simple Borrowing
- To borrow a value:
	- Prefix the value with `&`
- you can declare a reference variable, which borrows a value:
```rust
let s = String::from("linus");
let r = &s;

println!("{}, {}", s, r);
```
- `r` is a reference var
	- `r` borrows the value of `s`
	- `s` still owns the value
## Using Explicit Typing
- you can explicitly type a reference variable
	- prefix the data type with `&`
```rust
let s: String = String::from("torvalds");
let r: &String = &s;

println!("{}, {}", s, r);
```

- explicit typing is handy with functions
	- define reference parameters/returns
```rust
let mut s: String::from("Arch");
let r: &mut String =  &mut s;

r.push_str(" Linux");
println!("{}", r);
```