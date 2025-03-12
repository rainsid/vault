# Options for Passing Struct Parameters to a Function

- when you pass a (non-copy) struct by value to a function:
	- the called function receives ownership
	- the calling function loses ownership, and can't use the struct afterwards
- Generally, a better approach is to pass structs by reference instead:
	- the called function borrows the struct
	- the calling function retains ownership, and can use the struct afterwards

## Passing an Immutable Reference

- this function receives an immutable struct reference:
```rust
fn print_employee(e: &Employee){
	println!("{}", (*e).name); //explicit derefencing
	println!("{}", e.name); //implicit derefencing
}
```

- pass the struct by ref:
```rust
fn some_higher_level_function(){
	let e1 = Employee {... .. .. ..};
	print_employee(&e1);
}
```

## Passing a Mutable Reference

- this function receives an immutable struct reference:
```rust
fn reward_employee(e: &mut Employee){
	(*e).salary += 500; //explicit deref
	e.salary += 250; //implicit deref
}
```

- pass in a the struct by ref:
```rust
fn some_higher_level_function(){
	let e1 = Employee {... .. .. ..};
	print_employee(&mut e1);
}
```
