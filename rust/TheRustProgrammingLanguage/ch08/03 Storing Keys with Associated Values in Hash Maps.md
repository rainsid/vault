# Hash Map

- the type `HashMap<K, V>` stores a mapping of keys of type `K` to values of type `V` using a *hashing function*
- useful when you want to look up data not by using index but by using a key that can be of any type


## Creating a New Hash Map

- one way to create an empty hash map is to use `new` and to add elements with `insert`
```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);
```
 - hash map is not included in the prelude so we have to include it
 - like vectors hash maps are stored on the heap
 - hash map is homogeneous: all of the keys must have the same type
 
## Accessing Value in a Hash Map

- we can get a value out of the hash map by providing its key to the `get` method
```rust
fn main(){
	use std::collections::HashMap;

	let mut scores = HashMap::new();
	scores.insert(String::from("Blue"), 10);
	scores.insert(String::from("Yellow"), 50);

	let team_name = String::from("Blue");
	let score = scores.get(&team_name).copied().unwrap_or(0);
}
```
- the `get` method returns an `Option<&V>`
- if there is no value for that key, `get` will return `None`
- `copied` method is used to get an `Option<i32>` rather than `Option<&i32>` 
- `unwrap_or` is used to set `score` to zero if `scores` doesn't have an entry for that key

```rust
fn main(){
	use std::collections::HashMap;

	let mut scores = HashMap::new();
	scores.insert(String::from("Blue"), 10);
	scores.insert(String::from("Yellow"), 50);

	for (key, value) in &scores {
		println!("{key}: {value}");
	}
}

//prints

// Yellow: 50
// Blue: 10

```


## Hash Maps and Ownership

- for types that implement the `Copy` trait like i32, the values are copied into the hash map
- for owned values like `String`, the values will be moved and the hash map will be the owner of those values
```rust
use std::collections::HashMap;

let field_name =  String::from("Fave color");
let field_value = String::from("Blue");

let mut map = HashMap::new();
map.insert(field_name, field_value);

//field_naem and field_value are invalid at this point
```
- if we insert references to values into the hash map, the values won't be moved into the hash map
- the values that the references point to must be valid for at least as long as the hash map is valid


## Updating a Hash Map
- each unique key can only have one value associated with it a time
### Overwriting a Value

```rust
fn main(){
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Blue"), 20);

println!("{:?}", scores);

}
// {"Blue": 20}
```
- if we insert a key and a value in a hash map and then insert the same key with a different value, the value associated with that key will be replaced

### Adding a Key and Value Only if a Key Isn't Present

- it's common to check whether a particular key already exists in the hash map with a value and then to take the following actions: if the key does exist in the hash map, the existing value should remain the way it is; if the key doesn't exist, insert it and a value for it.
```rust
fn main(){
	use std::collections::HashMap;

	let mut scores = HashMap::new();
	scores.insert(String::from("Blue"), 10);

	scores.entry(String::from("Yellow")).or_insert(50);
	scores.entry(String::from("Blue")).or_insert(50);

	println!("{scores:?}");
}
// {"Blue": 10, "Yellow": 50}
```
- hash maps have a special API for this called `entry` that takes the key you want to check as a param
- the return value of the `entry` is an enum called `Entry` that represents a value that might or might not exist
- the `or_insert` method on `Entry` is defined to return a mutable reference to the value for the corresponding `Entry` key if that key exists, and if not, it inserts the param as the new value for this key and returns a mutable reference to the new value.

### Updating a Value Based on the Old Value

- hash maps common use case is to look up a keys' value and then update it based on the old value
```rust
fn main(){
	use std::collections::HashMap;

	let text = "hello hello world wonderful world";

	let mut map = HashMap::new();

	for word in text.split_whitespace(){
		let count = map.entry(word).or_insert(0);	
		*count += 1;
	}

	println!("{:?}",map);
}
// {"world": 2, "wonderful": 1, "hello": 2}
```
- the `split_whitespace` returns an iterator over sublslices, separated by whitespace, of the value `text`
- `or_insert` method returns a mutable reference (`&mut v`) to the value for the specified key
- that immutable reference is stored  in `count`
- in order to assign a value, we must first dereference `count` (`*count`)
- the mutable reference goes out of scope at the end of the `for` loop

## Hashing Function

- by default `HashMap` uses a hashing function called *SipHash* that can provide resistance to denial-of-service attacks involving hash tables
	- Siphash is not the fastest algorithm available, but the trade-off for better security that comes with the drop in performance is worth it
- if you profile your code and find that the default hash function is too slow, you can switch to another function by specifying a different hasher
