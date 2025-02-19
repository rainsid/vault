- you can pass reference params to a function
- the called function receives a reference
	- the call function *borrows* the value
- the calling function retains ownership 
	- the calling function can continue to use the value afterwards

# How to pass a reference Params

- to pass a reference parameter into a function:
	- precede the param with `&`

```rust
fn some_higher_level_func() {
	let n = 42;
	let s = String::from("hello");

	some_func(&n, &s);

	println!("{}", n); //ok
	println!("{}", s); //ok
}
```

# How to use reference Parameters

- when a function recieves a reference param:
	- use `*` to dereference, to obtain the underlying value
```rust
fn some_func(iparam: &i32, sparam: &i32){
	let n = *iparam;
	let s = (*sparam).to_uppercase();
}
```

- Rust actually allows a more direct syntax for invoking methods:
```rust
let s = sparam.to_uppercase();
```

# Passing `&String` Parameters

- if you declare a `&String` param:
	- you must pass in a `&String`
	- you can't pass i a `&str`
```rust
fn some_higher_level_func(){
	let s = String::from("hello");
	some_func(s); //ok
	some_func("hello") //no, cna't pass &str	
}

fn some_func(sparam: &String){
	//user sparam
}
```

# Passing `&str` Parameters

- if you declare a `&str` parameter:
	- you can pass in a `&String`
	- you can pass in a `&str`

```rust
fn some_higher_level_func(){
	let s = String::from("hello");
	some_func(&s); //ok, can pass &String
	some_func("hello"); //ok. can pass &str
}

fn some_func(sparam: &str) {
	//use sparam
}
```

--- 
## Aside : Displaying Reference Parameters

- when you have a reference param:
	- the default formatter *{}* displays the value
	- the print formatter *{:p}* displays the address (i.e., pointer)

```rust
fn some_function(iparam: &i32, sparam: &str) {
	//display values
	println!("{} {}", iparam, sparam);

	//display addresses
	println!("{:p} {:p}", iparam, sparam);
}
```








