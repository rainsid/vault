# Break
- You can use *break* to break out of a loop immediately
```rust
loop{
	if some_condition {
		break;	
	}
	...
}
```

- Typical usage:
	- Loop over a collection, looking for an item
	- Once you've found it, break out of the loop
----
# Continue
- you can use *continue* to continue to the next iteration:
```rust
loop{
	if some_condition{
		continue;	
	}

	...
}
```
- typical usage:
	- loop over a collection, processing item
		- if an item is invalid, skip it
---
## Controlling Nested Loops
- You can use *break* or *continue* in nested loops
- Label the outer loop. For example:
```rust
'outer: loop
```
- to break out of the loop:
```rust
break 'outer;
```
- to continue in the outer loop:
```rust
continue 'outer;
```