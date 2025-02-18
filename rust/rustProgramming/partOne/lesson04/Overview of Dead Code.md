# Dead code
- imagine you define enum ([[Understanding Enums]]), and make use of some (but not all) of the variants:
```rust
enum Color{
 Red, Green, Blue
}

...

let c: Color = Color: Red;

```
- The Rust compiler gives a warning about [[#Dead code]] for unused variants

## Allowing Dead Code
- To allow dead code, you can use the following attribute:
```rust
#[allow(dead_code)]
```
- you can apply this attribute to variants in an enum definition:
```rust 
enum Color{
	#[allow(dead_code)] Red,
	#[allow(dead_code)] Green,
	#[allow(dead_code)] Blue,
}
```