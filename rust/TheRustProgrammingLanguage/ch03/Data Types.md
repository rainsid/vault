- Rust is a *statically typed* language, which means that it must know the types of all vars at compile time
```rust 
let guess: u32 = "42".parse().expect("Not a number!");
```
- we'll get an error if we don't add `: u32` type annotation

# Scalar Types
- *Scalar* type represents a single value
	- [[integers]] ^345688
	- [[floating-point]]
	- [[booleans]]
	- [[characters]]

## Integer Types

- an *integer* is an number without a fractional component

**Int Types**

| **Length** | **Signed** | **Unsigned** |
| ---------- | ---------- | ------------ |
| 8-bit      | i8         | u8           |
| 16-bit     | i16        | u16          |
| 32-bit     | i32        | u32          |
| 64-bit     | i64        | u64          |
| 128-bit    | i128       | u128         |
| arch       | isize      | usize        |
- each signed variant can store numbers from -(2$^{2-1}$) to 2$^{n-1}$ - 1 inclusive where *n* is the number of bits that variant uses
- the `isize` and `usize` types depends on the architecture of the computer your program is running on
- int types default to `i32`

## Floating-Point Types
- *floating-point* numbers, are numbers with decimal points
- Rust floating-point types are `f32` and `f64` 
- the default type is `f64`
```rust
fn main(){
	let x = 2.0 //f64
	let y: f32 = 3.0 // f32
}
```


## Numeric Operations
- Rust supports the basic math operations: addition, subtraction, multiplication, division and remainder
- Integer division truncates toward zero to the nearest int
```rust
fn main() {
    let sum = 5 + 10;
    let diff = 95.5 - 4.3;
    let product = 4 * 30;
    let qoutient = 56.7 / 32.2;
    let truncated = 10 / 3;
    let remainder = 43 % 5;

    println!(
    "sum:{}, difference:{}, product:{}, qoutient:{}, truncated:{}, remainder:{}",
        sum, diff, product, qoutient, truncated, remainder
        );
}
```


## Boolean Type
- *Boolean* type has two possible values: `true` and `false`
- one byte in size
```rust
fn main(){
    let t = true; 
    let f: bool  = false; 
}
```
- main way to use *boolean* values is through conditionals

## Character Types
- *Char* literals are specified with single quotes
```rust 
fn main(){
   let c = 'z';
   let z: char = 'ℤ' // explicit type annotation
   let heart_eyed_cat = '😻';
}
```
- rust `char` type is four bytes in size and represents a Unicode Scalar Value


---

# Compound Types
- *Compound types* can group values into one type

## Tuple Type
- A *tuple* is a general way of grouping together a number of values with a variety of types into one
- it has a fixed length

```rust
fn main(){
   let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

- to get the values out of a tuple we use pattern matching to destructure a tuple value
```rust
fn main(){
   let tup = (500, 6.2, 1);
   let (x, y, z) = tup;
   println!("The of x, y, z: {}, {}, {}", x, y, z);
}
```

- we can also access an element directly using a period (`.`) followed by the index of the value we want to access
```rust
fn main(){
   let x: (i32, f64, u8) = (500, 6.4, 1);
   let five_hundred = x.0;
   let one = x.2;
}
```

- a tuple without any values has a name called *unit* 
- this value and it's corresponding type are both written `()` and represent an empty value or an empty return type


## A rray Type
- another way to have a collection of multiple values
- every element of an array must have the same type
- Rust array have a fixed length
```rust
fn main(){
    let a = [1,2,3,4,5];
}
```
- arrays are useful when you want your data allocated on the stack instead of the heap
- you write an array's type using square brackets with the type of each element, a semicolon, and then the number of elements in the array
```rust
let a: [i32, 5] = [1,2,3,4,5];
```
- you can also initialize an array to contain the same value for each element by specifying the initial value, followed by a semicolon, and then the length of the array in square brackets
```rust
let a = [3: 5]; //same as let a = [3,3,3,3,3];
```

### Accessing Array Elements
- you can access elements of an array using indexing
```rust
fn main(){
  let a = [1,2,3,4,5];
  let first = a[0];
  let second = a[1];
}
```

### Invalid Array Access
- accessing element past the end of the array results in runtime error
```rust
use std::io;

fn main() {
    let a = [1, 2, 3, 4, 5];

    println!("Enter an array index: ");

    let mut index = String::new();

    io::stdin()
        .read_line(&mut index)
        .expect("Failed to read line");

    let index: usize = index
        .trim()
        .parse()
        .expect("Index entered was not a number");

    let element = a[index];

    println!("The value of the element at index {index} is: {element}");
}
```

- entering 5 or greater is an invalid value