## Defining an Enum

```rust
enum IpAddrKind {
	V4, 
	V6,
}
```
- we can create an instance of each of the two variants of `IpAddrKind`
```rust
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```
- the variants are namespaced under its identifier using `::`
- we can put data into an enum variant, we attach data to variant of the enum directly
```rust
enum IpAddrKind {
	V4(String), 
	V6(String), 
}

let home = IpAddrKind::V4(String::from("127.0.0.1"));
let loopback = IpAddrKind::V6(String::from("::1"));
```

- each variant can have different types and amounts of associated data
```rust
enum IpAddr {
	V4(u8, u8, u8, u8),
	V6(String),
}

let home = IpAddr::V4(127, 0, 0, 1);
let loopback = IpAddr::V6(String::from("::1));
```

---
## Another example
``` Rust
enum Message {
	Quit,
	Move { x: i32, y: i32},
	Write(String), C
	ChangeColor(i32, i32, i32),
}
```
- this enum has four variants with diff types:
	- `Quit` has no data associated with it at all
	- `Move` has named fields, like a struct does
	- `Write` includes a single `String`
	- `ChangeColor` includes three `i32` values

- the ff structs could hold the same data 
```rust
struct QuitMessage;
struct MoveMessage {
	x: i32,
	y: i32,
}
struct WriteMessage(String);
struct ChangeColor(i32, i32, i32);
```

- we can also define methods on enums just like on structs
```rust
impl Message {
	fn call(&self) {
		// method body	
	}
}

let m = Message::Write(String::from("hello"));
m.call();
```

## The `Option` Enum and Its Advantages Over Null Values

- Rust has no null feature
- in other languages the concept of null is a value that is currently invalid or absent for some reason

- `Option<T>` is an enum that can encode the concept of a value being present of absent
```rust
enum Option<T> {
	None,
	Some(T),
}
```
- `Option<T>` is incluede in the prelude; no need to bring it to scope
- its variants are also included in the prelude: you can use `Some` and `None` withoud the `Option::` prefix
- the `<T>` syntax is a generic type param
	- it means that `Some` variant of the `Option` enum can hold one piece of data of any type
	- each concrete type that gets used in place of `T` make the overall `Option<T>` type a different type
```rust
let some_number = Some(5);
let some_char = Some('a');

let absent_number: Option<i32> = None;
```
- the type of `some_number` is `Option<32>`
- the type of `some_char` is `Option<char>`
- for `absent_number`, Rust requires to annotate the overall `Option` type (`Option<i32>`)
