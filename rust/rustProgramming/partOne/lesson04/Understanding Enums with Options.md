# [[Options]]
- rust defines a standard enum type name *Option*:

```rust
enum Option<T>{
	Some(T),
	None
}
```

- Option represents an optional value
	- Might contain a value of some type *T*
	- Or might contain no value at all

- Option is typically used as a function return type
	- indicates the return value might be empty
```rust
fn sec_of_day(h: 32, m:u 32, s: u32) -> Option<u32>{
	if h <= 23 && m <= 59 && s <= 59 {
		let secs = h * 3600 + m * 60 + s;	
		return Option::Some(secs);
	} else {
		return Option:None;	
	}
}
```

## Testing an Option Variable

- use *match* to test if an Option variable contains a value, and to extract that value

```rust
let sec: Option<u32>;

sec = sec_of_day(someHours, someMins, someSecs);

match sec{
	Some(s) => println!("Second of day: {}", s),
	None    => println!("Second of day: No value")
}
```

## Unwrapping an Option Variable
- Option defines a method named *unwrap_or()*
	- unwraps the value in an *Option*, if available
	- Otherwise returns the supplied default value
```rust
let sec: Option<32>

println!("Unwrapped sec: {}", sec.unwrap_or(0));
```

- Options defines many additional methods to help you process the value