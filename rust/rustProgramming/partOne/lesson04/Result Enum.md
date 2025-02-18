- Rust defines a standard enum type named [[Result]]:
```rust
enum Result<T, E>{
	Ok(T),
	Err(E)
}
```

- *Result* represents a value or an error
	- Might contain a value of some type *T*
	- Or might contain an error of some type E
- This is how Rust indicates and error
	- rather than via exceptions (like java, c++ etc.)

## Creating a Result Variable
- Result is typically used as a function return type
	- indicates the return might be OK or erroneous

- A good example is this function for i32:
	```rust
	from_str_radix(str, radix) -> Result<i32, ParseIntError>
	```
	
- The function return value will be:
	- Result::Ok\<i32\> or
	- Result::Err\<ParseIntError\>

## Testing a Result Variable

- use *match* ([[Flow Control#Matching]]) to get the value/error from a *Result* variable
```rust
let res: Result<i32, std::num::ParseIntError>;

res = i32::from_str_radix(someStr, 16);

match res{
	Ok(n) => println!("Parsed str as i32: {}", n),
	Err(e) => println!("Error occured: {}", e)
}
```

## Unwrapping a Result Variable
- Result defines a method named unwrap_or()
	- unwraps the value in a *Result*, if OK
	- otherwise returns the supplied default value, if error
	
```rust
let res2: Result<i32, std::num::ParseIntError>

println!("Unwrapped result: {}", res2.unwrap_or(1));
```

- Result defines many additional methods to help you process the value or error
