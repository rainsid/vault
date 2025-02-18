# Borrowing a `String` Object
```rust
let obj = String::from("hello");

let s = &obj;
```

- consider the types involved here ...
	- `&obj` - `&String`
	- `s` - `&String` (implicitly)
- `s` refers to the whole `String`

## Borrowing a `String` Object as `&str`
```rust
let obj = String::from("hello");

let s: &str = &obj;
```
- consider the types involved here...
	- `&obj` - `&String`
	- `s` - `&str` (explicitly)
- `s` is a *string slice*
	- could potentially be a sub-portion


### Implicit Type Coercions from `&String` to `&str`
- Rust allows implicit type coercion from `&String` to `&str`
	- if you borrow a `String` object (to obtain a `&String`)
	- you can assign it to a `&str` variable 
``` rust
let obj = String::from("hello");

let s: &str = &obj; //coerces &obj (type &String) to s (type &str)
```

- `&str` is handy with function params
	- can take a slice into any kind of string


## Borrowing a String Literal
- a string literal is a simple piece of fixed test
	`"hello"`

- technically speaking, a string literal is a string slice with static lifetime
```rust
let s: &'static str = "hello"
```

 