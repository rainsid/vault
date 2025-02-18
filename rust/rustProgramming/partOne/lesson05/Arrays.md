- An array is a fixed-size homogeneous collection collection
	- you can create an array using literal syntax \[a,b,c\]
	
- Declare the array as *mut* if you want to change its values
	- note, you can not change it's size

```rust
let a1 = [100, 101, 102] //fixed values
let mut a2 = [100, 101, 102] //mutable values
```

## Using an Array

- To access an element in an array
```rust
arr[index]
```

- Rust does bounds-checking at compile time and run time
	- the index must be 0 at length-1

- to get the length of an array:
```rust
arr.len()
```

- to iterate elements in an array:
```rust
for elem in arr { ... }
```

---
## Declaring an Array with a Type and Size
- You can declare an array with a specified type and size
	- use the syntax **\[type; size\]**
	
- You can then initialize the array when you're ready
	- You must supply the correct type and number of values

```rust
let a1: [i32; 5];

a1 = [100, 101, 102, 103, 104];
```

## Creating an Array with a Filler Value

- You can create an array with a filler value
	- Use the syntax **\[value; size\]**
	
- You can modify the data later if the array is *mut*

```rust
let mut a2 = [99; 5];

a2[0] = 23;
a2[4] = 42;
```

## Displaying an Array using the Debug Formatter

- Rust defines a trait named [[Debug]]
	- Has a *fmt()* function that formats data in a debug-friendly format

- Rust arrays implement *Debug*
	- So, arrays have fmt() function that formats array data nicely

- You can use the debug formatter like this:

```rust
println!("Array in debug format is {:?}", arr);
```