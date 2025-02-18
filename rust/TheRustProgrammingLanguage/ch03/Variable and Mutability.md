- by default, variables in rust are *immutable*
```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```
- we can make them mutable by adding `mut` in front of a variable name

## Constants

- *Constants* are values that are bound to name and are not allowed to change
- `mut` is not allowed to use in constants

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```
- *constants* are declared using the `const` keyword instead of the `let` keyword


## Shadowing
- you can declare a new var withe the same name as a previous var.
```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

- we can also change the type of the value
```rust
let spaces = "   ";
let spaces = spaces.len();
```

- if we use `mut` we will get a compile time error
```rust
let mut spaces = "  ";
let spaces = spaces.len(); // error: we are not allowed to mutate a var type
```