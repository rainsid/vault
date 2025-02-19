# How to Pass Mutable Reference Parameters

- to pass a mutable reference param into a function:
	- precede the parameter with `&mut`
``` rust
fn some_higher_level_function{
	let mut n = 42;
	let mut s = String::from("hello");

	some_func(&mut n, &mut s);

	println!("{}", n);
	println!("{}", s);
}
```

# How to User Mutable Reference Parameters

- when a function receives a mutable reference param
	- use `*` to dereference, to obtain/modify the underlying value
```rust
fn some_func(iparam: &mut i32) {
	*iparam += 10;

	(*iparam).push_str(" world");

	sparam.push_str("!"); //shorthand syntax
}
```