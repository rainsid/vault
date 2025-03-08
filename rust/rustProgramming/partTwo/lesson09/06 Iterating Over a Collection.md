# Overview

- Rust ha a standard type named `Iterator`
	- enables you to iterate over a collection
	- you can perform an operation on each element
	- you specify the operation as a closure
```rust
let v = vec!["c", "c++", "rust", "zig"];

println!("programming languages: ");

v.iter()
 .for_each(|e| println ("{}", e));
```

- Note:
	- `iter()` returns an `Iterator` object
	- `Iterator` has a `for_each` method
	- we pass a closure into `for_each`

## Aside: Unused Closure Variables

- if you have a closure that doesn't use a param, you can name the parameter `_` 
```rust
let v = vec!["c", "c++", "rust", "zig"];

println!("redacted programming languages: ");

v.iter()
 .for_each(|_| println!("xxx"));

```


## Filtering and Mapping Elements

- you can filter and map elements
```rust
let v = vec!["c", "c++", "rust", "zig"];

println!("uppercase 'c' pl");

v.iter()
	.filter(|e| e.starts_with('c'))
	.map(|e| e.to_uppercase())
	.for_each(|e| println!("{}", e));
```

## Collecting Results After Iteration

- you can collect results after iteration as follows:
```rust
let v = vec!["c", "c++", "rust", "zig", "typescript"];

let upper_t_pl = v.iter()
					.filter(|e| e.ends_with('t'))
					.map(|e| e.to_uppercase())
					.collect::<Vec<String>>();
```

- when you call `collect()`, you must specify what collection you want back
	- e.g., `collect::<Vec<String>>`