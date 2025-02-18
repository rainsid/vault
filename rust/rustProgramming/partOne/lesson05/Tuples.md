
# Tuple

- A tuple is a fixed-size heterogeneous collection
	- you can create a tuple using literal syntax (a, b ,c)

- Declare the tuple as *mut* if you want to change its values
	- you can't add/remove elements, or change their types

``` rust
let t1 = (9, "h1", 3.5); // fixed values

let mut t2 = (9, "hi", 3.5) //mutable values
```

## Using a Tuple

- To access an element, you must use a compile-time constant index like this:
	*tup.index*
	
- Rust does bounds-checking at compile-time
	- The index must be 0 to length-1

- There's is no way to determine the length, or to iterate through the elements:

```rust
tup.len()   // nope
for elem in tup   // nope
```

## Creating an Empty Tuple

- You can create an empty tuple, with no values
	- handy for functions that return nothing at all

```rust
let t3 = ();
```

## Declaring a Tuple with Element Types

- You can declare a tuple with specified element types
	- use the syntax *(type0, type1, type3)*

- you can then initialize the tuple when you are ready
	- you must supply the correct type and number of values

```rust
let t4: (i32, bool, f64);

t4 = (523, true, 23.2);
```

## Displaying a Tuple Using the Debug Formatter

- Rust tuples implement *Debug*
	- So, tuples have a *fmt()* function that formats data in a debug-friendly format

```rust
println!("Tuple in debug format is {:?}", tup);
```