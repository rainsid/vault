# Overview of Inheritance

- inheritance is an important feature in OO languages
	- define a supertype that specifies common members
	- define subtypes that inherit and extend the supertype

- inheritance in Rust is different to most other OO languages
	- Rust doesn't allow a struct to inherit from another struct
	- instead, inheritance in Rust is based on traits

## Example of Inheritance in Rust

- here is a trait that specifies overridable behavior:
```rust
trait Print {
	fn print(&self);
}
```

- here are some structs that implement it:
```rust
struct Point {...}

impl Print for Point {
	fn print(&self) {...}
}
```

```rust
struct Employee {...}

impl Print for Employee {
	fn print(&self) {...}
}
```

## The Liskov Substitution Principle

- Rust supports the Liskov Substitution Principle
	- declare a trait reference variable
	- the variable can refer to any object that implements the trait
```rust
let obj1 = Point::new(..);
let obj2 = Employee::new(..);

print_something(&obj1); //pass in &Point
print_something(&obj2); //pass in &Employee

fn print_something(p: &dyn Print){
	...
}
```

# Polymorphism

- the `dyn` keyword triggers dynamic dispatch
	- Rust dispatches the method dynamically at run time based on the type of object currently referenced
```rust
let obj1 = Point::new(..);
let obj2 = Employee::new(..);

print_something(&obj1); //pass in &Point
print_something(&obj2); //pass in &Employee

fn print_something(p: &dyn Print){
	p.print();
}
```

## Polymorphic Collections

- you can create a polymorphic collection in Rust
	- create a collection based on a trait type
	- the collection can hold any objects that implement the trait
	- method calls will be dynamically dispatched
```rust
let vec: Vec:<&dyn Print> = vec![&obj1, &obj2];

for obj in vec {
	obj.print();
}
```

