# Defining Default Methods in a Trait

- a trait can define default methods
	- i.e., methods that have a default implementation
		- can be optionally overridden in structs, if desired
```rust
trait log {
	fn log(&self);

	fn log_verbose(&self){
		print!("{} ", Utc::now());
		self.log();
	}
}
```

# Defining Associated Constants in a Trait

- a trait can define associated constants
	- i.e, constants associated with the interface
	- can be overridden in structs
```rust
trait Log {
	const LOG_TIMESTAMP: bool = false;
	...
}
```

## Accessing Associated Constants in a Trait 

- to access an associated constant in trait methods:
	- us the syntax `Self::CONSTANT_NAME`
```rust
trait Log {
	const LOG_TIMESTAMP: bool = false;

	fn log_verbose(&self) {
		if Self::LOG_TIMESTAMP {
			print!("{} ", Utc::now());
		}		
	self.log();
	}
}
```


## Implementing Multiple Traits in a Struct

- a struct can implement multiple traits
	- define a separate `impl` block for each trait implementation
```rust
struct Employee {
	...
}

impl Employee {
	...
}

impl Print for Employee {
	// implement Print trait here
}

impl Log for Employee {
	// implement Log trait here
}
```