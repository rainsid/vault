- this function receives two params, by value:
```rust
fn f1(iparam: i32, sparam: String){
	println!("{}", iparam);
	println!("{}", sparam);
}
```

- we can pass in arguments as follows:
```rust
fn some_higher_level_func(){
	let n =  42;
	let s = String::from("hello");

	f1(n,s); 
}
```

## Passing a Copyable Value

- when you pass a copyable value (e.g., i32):
	- Rust bit copies the value into the param
	- the original function retains ownership of the value
```rust
fn some_higher_level_func(){
	let n = 42;
	f2(n); // passes a copy
	println!("{}", n); // ok. we still own n
}

fn f2(iparam: i32){ // receives a copy
	println!("{}", iparam);  
}
```