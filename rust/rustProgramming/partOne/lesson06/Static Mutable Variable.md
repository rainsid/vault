- To access a static mutable variable, your code must be thread-safe
	- lock the variable, e.g., using a mutex
	- ensures only one thread can access the variable at a time
	- other threads block until the lock is released

---
## Defining Unsafe Code

- if you don't make your code thread-safe, you must explicitly mark it as *unsafe*:
```rust
unsafe fn some_unsafe_func(){
	static mut LOCAL_COUNT = 0i32;
	LOCAL_COUNT += 1;
}
```

- the caller must handle thread safety, or itself be marked as *unsafe*:
```rust
fn some_higher_level_func(){
	unsafe{
		some_unsafe_func();	
	}
}
```