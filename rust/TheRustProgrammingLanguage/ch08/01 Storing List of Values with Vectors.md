- Vector allows you to store more than one value in a single data structure
	- all the values are next to each other in memory
	- all values are of the same type

# Creating a New Vector

```rust
let v: Vec<i32> = Vec::new();
```
- type annotation is added because no values are inserted into the vector
- creating `Vec<T>` with initial values, Rust will infer the type of the value

```rust
let v = vec![1, 2, 3];
```
- `vec!` macro will create a new vector that holds the value you git it


# Updating a Vector

```rust
let mut v = Vec::new();

v.push(5);
v.push(6);
v.push(7);
v.push(8);
```
- use `push` method to add elements to a vector
- using `mut` makes the vector mutable

## Reading Elements of Vectors

- there are two ways to reference a value stored in a vector
	- via indexing
	- by using `get` method

```rust
let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2];
println!("The third element is {third}");

let third: Option<&i32> = v.get(2);
match third {
	Some(third) => println!("The third element is {third}"),
	None => println!("There is no third element");
}
```
- using `&` and `[]` gives us a reference to the element at the index value
- when the `get` method is used, we get an `Option<&T>`

-----
```rust
let v = vec![1, 2, 3, 4, 5];

let does_not_exist = &v[100];
let does_not_exist = v.get(100);
```
- the first method of accessing the element will cause the program to panic because it references a nonexistent element
- the `get` method returns `None` without panicking

---
```rust
let mut v = vec![1,2,3];

let first = &v[0];

v.push(6); // can not borrow `v`

println!("the first element is : {first}");
// this code won't compile
```
- we can't have mutable and immutable references of `v` in the same scope
- vectors put the values next to each other in memory, adding new element onto the end of the vector might require allocating new memory and copying the old elements to the new space, the reference  to the first element would be pointing to deallocated memory

## Iterating Over the Values in a Vector

```rust
let v = vec![100, 32, 54];
for i in &v {
	println!("{i}");
}
```
- we would iterate through all of the elements rather than use indices to access one at a time

```rust
let mut v = vec![100, 32, 54];

for i in &mut v {
	*i += 50;
}
```
- to change the value that the mutable reference refers to , we have to use the `*` operator to get to the value in `i`
- iterating over a vector, whether mutably or immutably, is safe because of the borrow checker's rules
- if an *insert* or *remove* is attempted, we would get a compiler error 

# Using an Enum to Store Multiple Types

```rust
enum SpreadsheetCell {
	Int(i32),
	Float(f64),
	Text(String)
}

let row = vec![
	SpreadsheetCell::Int(3),
	SpreadsheetCell::Text(String::from("blue"),
	SpreadsheetCell::Float(10.12),
];
```

- variants of an enum are defined under the same enum type
- we can define an enum whose variants will hold different value types and all the enum variants will be considered the same type
- then create a vector to hold the enum

# Dropping a Vector Drops Its Elements

- like any other struct, a vector is freed when it goes out of scope
```rust
{
	let v = vec![1,2,3];
	// do stuff with v
} // <- v goes out of scope and is freed here
```
- when the vector gets dropped, all of its contents are also dropped