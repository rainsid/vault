# Iterating Over an Array Slice
- an array slice knows:
	- the address of an element in an array
	- the number of elements in in the slice

- you can iterate over the elements in an array slice:
```rust
let a = [10, 11, 12, 13, 14];

let s = &a;

for elem in s {
	println!("{}", elem);
}
```


## Creating a Slice as a Portion of an Array

- you can create a slice as a portion of an array
	- specify the start and end indexes (as element positions)
	- the start is inclusive (default is 0)
	- the end index is exclusive (default is to end of array)

```rust
let a = [10, 11, 12, 13, 14, 15];
//let r1 = &a[<start_index> .. <end_index>];
let r1 = &a[2..4];
```

## Creating a Mutable Array Slice
- you can define a mutable array slice
	- declare as `&mut [aType]`
```rust
let mut a = [10, 11, 12, 13, 14];

let s: &mut [i32] = &mut a[2..4];

s[0] = 130;
```