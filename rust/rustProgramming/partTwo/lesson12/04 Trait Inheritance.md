# Overview
- Rust allows you to define a hierarchy of traits
	- a trait can inherit from other traits
	- this enables you to specify a cumulative interface
 ![[deque_inherits_queue.png]]

## How to Define a Hierarchy of Traits

- here's a `Queue`, the supertrait:
```rust
trait Queue {
	fn len(&self) -> usize;
	fn push_back(&mut self, n: i32);
	fn pop_front(&mut self) -> Option<i32>;
}
```

- here's `Deque`, the subtrait:
```rust
trait Deque : Queue {
	 fn push_front(&mut self, n: i32);
	 fn pop_back(&mut self) -> Option<i32>;
}
```

## How to Implement a Hierarchy of Traits

- if a struct implements a trait:
	- it must also implement all supertraits
- here's a struct that implements `Deque`
	- it also implements the supertrait, `Queue`
```rust
struct MyDeque {...}

impl Queue for MyDeque {...}
impl Deque for MyDeque {...}
```













