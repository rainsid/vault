```rust
fn main(){
	panic!("crash and burn");
}
```

- two ways to cause panic in practice
	- by taking an action that causes code to panic (such as accessing an array past the end)
	- explicitly calling the `panic!` macro
