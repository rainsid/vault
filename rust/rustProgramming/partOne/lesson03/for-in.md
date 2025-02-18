- Rust has a *for-in* loop, to iterate over a collection:
``` rust
let arr = [99, 55, 22, 33, 44, 100];

for elem in arr {
	println!("{}", elem);
}
```
- you can use *for-in* to iterate over a numeric range
- here is a loop with an exclusive upper limit:
```rust 
for i in 0..10{
	println!("{}", i); //0 up to 9
}
```
- and an inclusive upper limit:
```rust 
for i in 0..=10{
	println!("{}", i); // 0 up to 10
}
```