
- HashMap<K,V>
	- a generic dictionary
	- each entry is a key/value pair

- to create a HashMap object:
```rust
let mut m: HashMap<String, i32> =  HashMap::new();
//or
let mut m = HashMap::<String, i32>::new();
```

- note: there is no equivalent to *vec!* to create and initialize a HashMap

## Inserting an Item
- You can insert an item like this
	- if the key already exists, its value is overwritten
	```rust
	m.insert(aKey, aValue);
	```
- if you want to insert an item only if the key doesn't already exist:
	```rust
	m.entry(aKey).or_insert(aValue);
```

## Looking up a key

- you can look up a key in a HashMap, to get the value:
	`let val = m[aKey];`
- if the key is missing the program panics
	- i.e, it crashes with an error message

## Looking up a key Safely

- if you are not sure if the key is present, you can do a safe look-up as follows:
	```rust
	let opt = m.get(aKey); // returns an Option<V>`
```

- You can then test the `Option\<V\>` to see if it contains a value (or none)
```rust 
match opt{
	Some(v) => println!("Value: {}", value),
	None => println!("No value")
}
```

## Iterating Over Items
- You can iterate over the items of a *HashMap*
```rust
for entry in &m {
	// stattements go here
}
```

- On each iteration, you obtain an *Entry*
	- Contains a *key* and a *value*

- Note the *&* prefix on the map variable
	- this is another example of [[Borrowing]]
	- prevents the map from being emptied


## Displaying a HashMap Using the Debug Formatter

- The *`Hashmap<K,V`* type implement *Debug*

- So, you can use the debug formatter to output its data all at once
```rust
println!("Map in debug format is {:?}", m);
```