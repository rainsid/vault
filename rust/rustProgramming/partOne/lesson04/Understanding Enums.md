# Enums
- an enum is a type with a closed set of values
	- example, a *Flight* enum might allow **Economy**, **Business**, **First**
	
- enums are very important and are used widely in Rust
	- both in the Rust lib, and in the code we write ourselves

---
## Defining an Enum Type:
- specify the enum type, starting with capital
- specify allowed values ([[variants]]), also starting with capitals

```rust
enum Color{
	Red,
	Gree,
	Blue
}
```

- to use an enum type:
	- use the enum type, followed by ::, followed by a variant
	- you often use *match* ([[Flow Control#^dc7c24]]) to test variant values
```rust
let c: Color = Color::Red;
match c {
	Color::Red => println!("coch"),
	Color::Green => println!("gwyrdd"),
	Color::Blue => println!("glas"),
}
```

---
## Defining Enums in a Separate File
- it's common to define enums in a separate file:

```rust
pub enum Color{ // make it public so it can be used in other files
	Red, Green, Blue
}

// mytype.rs
```

- you load the module into *main.rs*, and introduce symbols into scope:
```rust
// load the module
mod mytypes;

// introduce the Color type into the scope
use mytypes::Color;
```

## Defining and using enums with data
- enum types like this are essentially just a simple flag:
```rust
enum Color{
	Red, Green, Blue
}
```

- it is possible to associate data with variants in an enum type
```rust
enum HouseLocation {
	Number(i32),
	Name(String),
	Unknown
}
```

- An enum contains the specified data
	- Depending on the current variant value

- We can create an enum variable like this:
```rust
let h1 = HouseLocation::Number(4);
```

```rust
let h2 = HouseLocation::Name("Cartref");
```

```rust
let h3 = HouseLocation::Unknown;
```

- To get data out of an enum variable, use *match*([[Flow Control#Matching]])
```rust
let h: HouseLocation = ...;

match h {
	HouseLocation::Number(n) => println!("Number is {}", n),
	HouseLocation::Name(s) => println!("Name is {}", s),
	HouseLocation::Unknown => println!("Unknown")
}
```

## Understanding how Enums with Data Work
- When you define an enum type with data:
	- The type is large enough to store any of the values
	- i.e., it is large enough to hold the biggest variant value

- You can determine the size as follows:
```rust 
let size = std::mem::size_of::<HouseLocation>();
```

































