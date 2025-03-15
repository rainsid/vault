# Defining Mutable Methods

- if you want to allow a method to modify an instance, define `self` as a mutable reference
- you can use full syntax
```rust
fn reset (self: &mut Point){
	self.x = 0;
	self.y = 0;
}
```

- or you can write either of these ways:`
```rust
fn reset (self: &mut Self){...} //use self alias

fn reset (&mut Self){...} //shorthand
```


## Invoking Mutable Methods

- you can only invoke mutable methods upon objects that are defined as mutable objects
- so this will work
```rust
let mut p1 = Point {x: 10, y: 10};
p1.reset();
```
- this won't
```rust
let p2 = Point {x: 10, y: 10};
p2.reset();
```