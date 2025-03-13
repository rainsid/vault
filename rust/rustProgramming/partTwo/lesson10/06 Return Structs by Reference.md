# Overview

- you can return a struct by reference from a function
	- the caller can then use the reference that you return
- Note: you can't return a reference to a local stack-based object
	- this would be a dangling reference

## A common Scenario

- here's a common scenario for returning a reference:
```rust
fn some_func(<objects by ref>) -> <return reftype> {
	return <reference to one of the objects passed in>
}
```

```rust
fn some_higher_level_func() {
	//create some objects here
	let ref = some_func(<pass objects by ref>);
	//use the ref returned by some_func()
}
```

## Returning a Reference: Incorrect Approach

```rust
fn choose_employee(e1: &Employee, e2: &Employee) -> &Employee {
	if e1.salary > e2.salary { e1 } else { e2 }
}
```

- this function attempts to return either reference `e1` or `e2`
	- `e1` and `e2` might have different lifetimes
	- so the compiler doesn't know how long the reference return will be valid for

## Returning a Reference: Correct Approach

```rust
fn choose_employee<'a>(e1: &'a Employee, e2: &'a Employee) -> &'a Employee {
	if e1.salary > e2.salary { e1 } else { e2 }
}
```

- `<'a>` is a lifetime annotation
	- we apply `'a` to each reference param and to the reference return
	- this indicates they all have the same lifetime

## Returning a Mutable Reference

- it's quite straightforward to return a mutable reference:
```rust
fn choose_employee<'a>(e1: &'a mut Employee, e2: &'a mut Employee) -> &'a mut Employee {
	if e1.salary > e2.salary { e1 } else { e2 }
}
```