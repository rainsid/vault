- an array slice can borrow some (or all) of an array:
	- prefix the array with `&`

```rust
let a = [100, 101, 102, 103, 104];

let s = &a;
```

- `s` is an *array slice*
	- borrows the whole array

## Explicitly Typing an Array Slice

- you can explicitly type an array slice
	- specify a type name such as `&[aType]`
```rust
let a = [100, 101, 102, 103, 104];

let s: &[i32] =  &a;
```

## What info does an Array Slice Contain?

- an array slice refers to some (or all) data in an array
- an array slice contains two pieces of info:
	- the address of an element in the array
	- the length of the slice, in elements

```rust
let a = [10, 11, 12, 13, 14];
let b = &a;

println!("{:p}, {}, {:?}", b.as_ptr(), b.len(), b);
```