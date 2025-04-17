- we use generics to create definitions for items like function signatures or structs, which we can then use with many different concrete data types

# In Function Definitions

- when defining a function that uses generics, we place the generics in the signature of the function where we would usually specify the data types of the params and return val

- we have to declare the param name in the signature so the compiler knows what that name means
- we have to declare the type param name before we use it
```rust
fn largest<T>(list: &[T]) -> &T {
}
```

----
```rust
fn largest<T>(list: &[T]) -> &T {
	let mut largest = &list[0];

	for item in list {
		if item > largest {
			largest = item;		
		}	
	}

	largest
}

fn main() {
	let number_list = vec![34, 50, 25, 100, 65];

	let result = largest(&number_list);
	println!("the largest number is {result}");

	let char_list = vec!['y', 'm', 'a', 'q'];

	let result = largest(&char_list);
	println!("The largest char is {result}");
}
```

- if we compile this get, we will get an error
```bash
$ cargo run
   Compiling chapter10 v0.1.0 (file:///projects/chapter10)
error[E0369]: binary operation `>` cannot be applied to type `&T`
 --> src/main.rs:5:17
  |
5 |         if item > largest {
  |            ---- ^ ------- &T
  |            |
  |            &T
  |
help: consider restricting type parameter `T`
  |
1 | fn largest<T: std::cmp::PartialOrd>(list: &[T]) -> &T {
  |             ++++++++++++++++++++++

For more information about this error, try `rustc --explain E0369`.
error: could not compile `chapter10` (bin "chapter10") due to 1 previous error

```
- this error states that the body of `largest` won't work for all possible `T` could be
- we can only use types whose values can be ordered.
- to enable comparisons, the std lib has the the `std::cmp::PartialOrd` trait that you can implement on types


---

# In Struct Definitions

- we can also define structs to use a generic type param in one or more fields using the `<>` syntax
```rust
struct Point<T> {
	x: T,
	y: T
}

fn main(){
	let integer = Point {x: 5, y: 4};
	let float = Point {x: 5.3, y: 4.3};
}
```
- the syntax for using generics in struct definitions is similar to that used in function definitions

```rust
struct Point<T> {
	x: T,
	y: T
}

fn main(){
	let wont_work = Point {x: 5, y: 4.34};
}
```
- this code won't compile because the struct definition says that the `Point<T>`struct is generic over some type `T`
- the fields `x` and `y` are *both* that same type
- when we assign the int val `5` to `x`, we let the compiler know that the generic type `T` will be an int for the instance of `Point<T>`, then we specify `4.0` for `y`, we'll get a type mismatch error

```rust
struct Point<T, U> {
	x: T,
	y: U,
}

fn main(){
	let both_integer = Point {x: 5, y: 10};
	let both_float= Point {x: 5.32, y: 10.33};
	let int_and_float = Point {x: 32, y: 3.2};
}
```
- we can use multiple generic type params to define a `Point` struct where `x` and `y` are both generics but could have diff types

----

# In Enum Definitions

- we can define enums to hold generic data types in their variants
```rust
enum Option<T> {
	Some(T), 
	None,
}
```
- the `Option<T>` enum is generic over type `T` and has two variants: `Some`, which holds one value of type `T`, and a `None` variant that does not hold value
- by using the `Option<T>` enum, we can express the abstract concept of an optional value, and because `Option<T>` is generic, we can use this abstraction no matter what the type of the optional value is

- enums can use multiple generic types as well
```rust
enum Result<T, E> {
	Ok(T),
	Err(E)
}
```
- the `Result` enum is generic over two types, `T` and `E` and has two variants: `Ok`, which holds a value of type `T`, and `Err` which holds a value of type `E` 
- this definition makes it convenient to use the `Result` enum anywhere we have an operation that might succeed (return a value of some type `T`) or fail (return an error of some type `E`)


----

# In Method Definitions

- we can implement methods on structs and enums and use generic types in their definitions too
```rust
struct Point<T> {
	x: T,
	y: T,
}

impl<T> Point<T> {
	fn x(&self) -> &T {
		&self.x	
	}
}

fn main(){
	let p = Point {x: 5, y: 10};

	println!("p.x = {}", p.x());
}
```
- we have to declare `T` just after `impl` so we can use `T` to specify that we're implementing methods on the type `Point<T>`
- by declaring `T` as a generic type after `impl`, Rust can identify that the type in the angle brackets in `Point` is a generic type rather than a concrete type
- by convention we use the same name for the generic param declared in the struct definition
- if you write a method within an `impl` that declares a generic type, that method will be defined on any instance of the type, no matter what concrete type ends up substituting for the generic type


- we can also specify constraints on generic types when defining methods on the type
```rust
impl Point<f32> {
	fn distance_from_origin(&self) -> f32 {
		(self.x.powi(2) + self.y.powi(2)).sqrt()
	}
}
```
- this code means the type `Point<f32>` will have a `distance_from_origin` method; other instances of `Point<T>` where `T` is not of type `f32` will not have this method defined 


```rust
struct Point<X1, Y1> {
	x: X1,
	y: Y1,
}

impl<X1, Y1> Point<X1, Y1> {
	fn mixup<X2, Y2>(self, other: Point<X2, Y2>) -> Point<X1, Y2> {
		Point {
			x: self.x,
			y: other.y,	
		}	
	}
}

fn main(){
	let p1 = Point {x: 5, y: 10.4};
	let p2 = Point {x: "hello", y: 'c'};

	let p3 = p1.mixup(p2);

	println!("p3.x = {}, p3.y = {}", p3.x, p3.y);
}
```
- the purpose of this example is to demonstrate a situation in which some generic params are declared with `impl` and some are declared with the method definition
- the generic params `X1` and `Y1` are declared after `impl` because they go with the struct definition
- the generic params `X2` and `Y2` are declared after `fn mixup` because they're only relevant to the method 
----

# Performance of Code Using Generics

- using generic types won't make your program run any slower than it would with concrete types
- *monomorphization* is the process of turning generic code into specific code by filling  in the concrete types that are used when compiled
- the compiler looks at all places where generic code is called and generate code for the  concrete types the generic code is called with

```rust 
let integer = Some(5);
let float = Some(5.0);
```
- when Rust compiles this code, it performs monomorphization
- the compiler reads the values that have been used in `Option<T>` instances and identifies two kinds of `Option<T>`: one is `i32` and the other is `f64`
- it expands the generic definition of `Option<T>` into two definitions specialized to `i32` and `f64`
- the monomorphized version of the code looks similar to the ff:
```rust
enum Option_i32 {
	Some(i32),
	None,
}

enum Option_f64 {
	Some(f64),
	None,
}

fn main(){
	 let integer = Option_i32::Some(5);
	 let float = Option_f64::Some(5.0);
}
```
- the generic `Option<T>` is replaced with the specific definitions created by the compiler
- it performs just as it would if we had duplicated each definition by hand


























