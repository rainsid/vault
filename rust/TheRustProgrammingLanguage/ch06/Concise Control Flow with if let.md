- `if let` syntax lets you combine `if` and `let` into a less verbose way to handle values that match one pattern while ignoring the rest
```rust
let config_max = some(u8);

if let Some(max) = config_max {
	println!("The maximum is configured to be {max}");
}
```
- the `if let` take a pattern and an expression separated by an equal sign
- the code above is equivalent to:
```rust
let config_max = Some(3u8); 
match config_max { 
	Some(max) => println!("The maximum is configured to be {max}"), 
	_ => (), 
}
```

- we can include an `else` with an `if let`
- the block of code that goes with the `else` is the same as the block of code that would go with the `_` case in the `match` expression that is equivalent to the `if let` and `else` 
```rust
let mut count = 0;
if let Coin::Quarter(state) = coin {
	println!("State quarter from {state:?}!");
} else {
	count += 1;
}
```