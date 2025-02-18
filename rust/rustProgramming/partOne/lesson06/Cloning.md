# Understanding the `Clone` Trait
 - Rust defines a trait named `Clone`
	 - has a `clone()` function
	 - returns a clone (copy) of an object's value
- the `String` type implements `Clone`
	- you can call `clone()` on a `String`
	- returns a `String` with a copy of the text
	- you can still use the original `String`
- example
``` rust
let mut s1 = String::from("hello");
let s2 = s1.clone();
s1.push_str(" world");

println!("{}", s1); // "hello world"
println!("{}", s2); // "hello"
```


