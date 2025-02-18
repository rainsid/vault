- Rust defines several atomic data types
	- thread-safe wrappers around primitive values
	- e.g, `AtomicI8`, `AtomicU8`, `AtomicBool`, etc.
- Atomic data types enable you to modify primitive values atomically
	- the atomic types lock values implicitly
	- thread-safe out-of-the-box

```rust
use std::sync::atomic::{AtomicI32, Ordering};
...
fn some_func(){
	static LOCAL_COUNT: AtomicI32 = AtomicI32::new(0);

	LOCAL_COUNT.fetch_add(1, Ordering::Relaxed);

	println!("{:?}", LOCAL_COUNT);
}
```