# Creating a Struct Instance

- to create a struct instance:
	- use the struct name, followed by `{}`
	- inside the `{}`, initialize all fields (in any order)
```rust
let e1 = Employee {
	name: String::from("Jane");
	salary: 1000,
	fulltime: true
}
```

- struct instances are stack-allocated

## Creating a Mutable Struct Instance

- to create a mutable struct instance:
	- use the `mut` keyword in the variable declaration
```rust
let mut e2 = Employee {
	name: String::from("Jane");
	salary: 1000,
	fulltime: false
}
```

- mutability applies to the whole object not on a field-by-field basis

## Accessing fields in a Struct Instance

- use the syntax `anInstance.aField`
```rust
let e1 = Employee {... ... ...};

println!("{} {} {}", e1.name, e1.salary, e1.fulltime);
```

- if the struct variable is declared as `mut`, you can modify any field
```rust
let mut e2 = Employee {... .. .. };

e2.salary *=2;

println!("{} {} {}", e1.name, e1.salary, e1.fulltime);

```