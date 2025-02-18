- It's possible to define a *static global* variables
	- accessible by all functions

- The rules are the same as for static locals:
	- use the `static` keyword
	- specify the variable name, in CAPS
	- specify the data type
	- supply a value, typically a constant
```rust
static MESSAGE: &str = "Hello";
```

## Accessing Global Static Variables on Other Modules

- You can make a global variable visible to other modules 
	- declare the global variable as `pub`
```rust
pub static MESSAGE: &str = "Hello";
```
- To access the variable in another module:
	- declare the sub-module
	- optionally import the variable name
```rust
mod module1;
use module1::MESSAGE;
....
println!("{}", MESSAGE);
```

## Initializing a Global Variable Lazily

- You can initialize a global variable lazily, via `Lazy<T>`
``` rust
static GLOBAL_TIMESTAMP: Lazy<DateTime<Utc>> = Lazy::new(|| Utc::now());
```
- the *Lazy* object is thread-safe wrapper around the value
- the *initialization code* runs once, upon first usage of the variable