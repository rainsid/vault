- Rust compiler has a *borrow* checker
	- enforces Rust's strict rules for borrowing
- The borrow checker enforces these rules:
	- single writer (mutable borrow)
	- many readers (immutable borrow)

## Defining Many Immutable References
- you can define many immutable references to a value
	- immutable references can't modify the value
	- so this is guaranteed to be safe

```rust
let s = String::form("hello");

let r1 = &s;
let r2 = &s;
let r3 = &s;

println!("{}, {}, {}", r1, r2, r3);
```

## Restrictions after Defining a Mutable Reference

- Imagine you define a mutable reference `r1`
	- `r1` is allowed to modify the underlying value
	
- you can't define another mutable reference `r2`
	- `r2` might modify the underlying value
	- this might interfere with `r1`

- you can't define an immutable reference `r3`
	- the underlying value could change via `r1`
	- so the value of `r3` would seem to change

## Restrictions after Defining an Immutable Reference

- imagine you define an immutable reference `r1`
	- `r1` is not allowed to modify the underlying value
- you can't define a mutable reference `r2`
	- `r2` might modify the underlying value
	- so the value of `r1` would seem to change