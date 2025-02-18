# Vector

- *`Vect<T>`* is a generic, sequential, re-sizable collection
	- Defined in the *`std::vec`* module (imported automatically)

- To create a *Vec* object explicitly:
```rust
let mut v: Vec<i32> = Vec::new();

//or 

let mut v = Vec::<i32>::new();

// alternatively, you can create a Vec object and
// initialize it via vec!

let mut v  = vec![100, 101, 102];
```

---

## Indexing into a Vec

- You can acces an item in a *Vec* as follows:
	`let item = v[index]`

- when you use [], rust does runt-time bound-checking
	- if the index is invalid, the program panics (throws an exception)
	- i.e, it crashes with an error message

---
### Indexing Safely into a Vec

- If you're not sure if the index is valid, you can access an item in a Vec safely as follows:
```rust
let opt = v.get(index); //REturns Option<T>
```

- You can test the *Option* to see if it contains a value (or none)

```rust
match opt {
	Some(n) => println!("Value: {}", value);
	None => println!("No value");
}
```

## Adding and Removing Items

- *`Vec<T>`* has many methods to add and remove items
```rust
v.push(item);

let item = v.pop();

v.insert(index, item);

let length = v.len();
```

## Iterating Over Items

- you can iterate over the items of a Vec:
```rust
for item in &v{
	// statements here
}
```

- Note the *`&`* prefix on the *Vec* variable
	- this is known as *[[Borrowing]]* in Rust
	- This is necessary, otherwise the Vec contents will be emptied in the loop

## Displaying a Vec Using the Debug Formatter

- The *`Vec<T>`* type implements *Debug*

- So you can use the debug formatter to output its data all at once
```rust
println!("Vector in debug format is {:?}", v);
```