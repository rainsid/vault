# Overview of Associated Data
- Rust also lets you define *associated data*
	- data that pertains to the entire struct type
	- effectively, data that's shared by all instances

- there are two ways to define associated data:
	- constant data
	- non-constant (static) data

# Defining Constant Associated Data

- to define and use constant associated data:
	- define a `const` in the `impl` block (optionally public)
	- use the `const` data in your functions
```rust
pub struct Employee {
	...
}

impl Employee {
	const MAX_SALARY: u64 = 99_000;

	pub fn payrise(&mut self, amount: u64){
		self.salary += amount;
		if self.salary > Employee::MAX_SALARY {
			self.salary = Employee::MAX_SALARY; }
	}
}

//mytypes/employee.rs
```

## Defining Non-Constant Associated Data

- to define and use non-constant (static) associated data:
	- define a `static` variable in the module (not in `impl` block)
	- use the `static` variable in your functions
```rust
pub struct Employee {...}

static NEXT_ID: AtomicI32 = AtomicI32::new(0);

impl Employee {
	pub fn new {... ... ...} -> Employee {
		let id = NEXT_ID.fetch_add(1, Ordering::Relaxed);
	}
}
//mytypes/employee.rs
```

