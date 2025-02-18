- to define a struct, we enter the keyword `struct` and name the entire struct.
```rust
struct User{
	active: bool,
	username: String,
	email: String,
	sign_in_count: u64,
}
```

- struct holds multiple related values that can be of different types

- to use a struct after defining it, we create an *instance* of that struct by specifying concrete values of the fields
```rust
fn main(){
	let user1 = User{
		active: true,
		username: String::from("user1234"),
		email: String::from("email@example.com"),
		sign_in_count: 1,
	};
}
```

- to get a specific value from a struct, we use dot notation
	- if the instance is mutable, we can change a value by using the dot notation and assigning into a particular field
```rust
fn main(){
	let mut user1 = User{
		active: true,
		username: String::from("user1234"),
		email: String::from("email@example.com"),
		sign_in_count: 1,
	};

	user1.email = String::from("anotheremail@example.com");
}
```

- the `build_user` function returns a `User` instance with the given email and username. The `active` field gets the value of `true`, and the `sign_in_count` gets a value of `1`
```rust
fn build_user(email: String, username: String) -> User {
	User {
		active: true,
		username: username,
		email: email,
		sign_in_count: 1
	}
}
```

## Using the Field Init Shorthand

- because the parameter names and the struct field names are exactly the same, we can use the *field init shorthand* syntax to rewrite `build_user` so it behaves exactly the same but doesn't have the repetition of `username` and `email`
```rust
fn build_user(email: String, username: String) -> User {
	User{
		active: true,
		username,
		email,
		sign_in_count: 1	
	}
}
```

## Creating Instances from Other Instances with Struct Update Syntax

- by using *struct update syntax* we can create a new instance of a struct that includes most of the values from another instance
```rust
fn main(){
	// --snip--
	let user2 = User{
		active: user1.active,
		username: user1.username,
		email: String::from("another@example.com"),
		sign_in_count: user1.sign_in_count,
	};
}
```
- we can achieve the same effect with less code using *struct update syntax*
- the syntax `..` specifies that the remaining fields not explicitly set should have the same value as the fields in the given instance
```rust
fn main(){
	// --snip--
	let user2 = User {
		email: String::from("another@example.com"),
		..user1
	};
}
```

## Using Tuple Structs Without Named Fields to Create Different Types

- *Tuple Structs* have the added meaning the struct name provides but don't have names associated with their fields
- to define a tuple struct, start with the `struct` keyword and the struct name followed by the types in the tuple
```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
	let black = Color(0, 0, 0);
	let origin = Point(0, 0, 0);
}
```

## Unit like Structures Without Any Fields

- you can define structs that don't have any fields, these are called *unit-like structs*
```rust
struct AlwaysEqual;

fn main() {
	let subject = AlwaysEqual;
}
```

