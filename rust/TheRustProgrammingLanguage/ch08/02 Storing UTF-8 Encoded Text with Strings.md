# What is a String

**String**
- is a type provided by Rust's standard lib rather than coded into the core language
- is growable, mutable, owned, UTF-8 encoded string type

---

## Creating a New String

```rust
let mut s = Sting::new();
```
- same way with `Vec<T>`, `String` also uses the `new` function to create an instance

```rust
let data = "initial contents";

let s = data.to_string();

// the method also works on string literal
let s = "initial contents".to_string();
```
- we can also use `to_string` on string literals

```rust
let s = String::from("initial contents");
```
- we can also use the function `String::from` to create a `String` from a string literal

---

## Updating a String

- a `String` can grow in size and its contents can change
- you can use the `+` operator or the `format!` macro to concatenate `String` values
### Appending to a String with `push_str` and `push`

- we can grow a `String` by using the `push_str` method to append a string slice
```rust
let mut s = String::from("foo");
s.push_str("bar");
```

- `push_str` method takes a string slice because we don't necessarily want to take ownership of the param
```rust
let mut s1 = String::from("foo");
let s2 = "bar";
s1.push_str(s2);
println!("s2 is {s2}");
```

- `push` method takes a single char as a param and adds it to the `String`
```rust
let must s = Sting::from("lo");
s.push('l');
```

### Concatenation with the `+` Operator or the `format!` Macro

- using the `+` operator
```rust
let s1 = String::from("Hello, ");
let s2 = String::from("world");
let s3 = s1 + &s2; // s1 has been moved here and can no longer be used
```
- the reason `s1` is no longer valid after the addition, and the reason we used a ref to `s2`, has to do with the signature of the method that's called when we use the `+` operator
- the `+` operator uses the `add` method, whose signature looks something like this:
```rust
fn add(&self, s: &str) -> String {}
```

- we can use `format!` macro as an alternative to `+` 
```rust
```rust
let s1 = String::from("tic");
let s2 = String::from("tac");
let s3 = String::from("toe");

let s = format!("{s1}-{s2}-{s3}");
```

### Indexing into Strings
- Rust strings don't support indexing

### Internal representation

- a `String` is a wrapper over a `Vec<u8>`
```rust 
let hello = "Здравствуйте";
let answer = &hello[0] 

//this won't compile
```
- the string length is 24
- each unicode scalar value in "Здравствуйте" takes 2 bytes 
- when encoded in UTF-8, the first byte of `З` is `208` and the second is 151

### Bytes and Scalar Values and Grapheme Clusters

- there are actually three relevant ways to look at strings from Rust's perspective
	- as bytes
	- scalar values
	- grapheme clusters

- the Hindi word “नमस्ते” is stored as a vector of `u8`
```text
[224, 164, 168, 224, 164, 174, 224, 164, 184, 224, 165, 141, 224, 164, 164,
224, 165, 135]
```

- if we look at them as unicode scalar value, which are what Rust's `char` type is, those bytes look like this:
```text
['न', 'म', 'स', '्', 'त', 'े']
```
- there are six `char` values here, but the fourth and the sixth are not letters: they're diacritics that don't make sense on their own
- if we look at them as grapheme clusters:
```text
["न", "म", "स्", "ते"]
```

### Slicing Strings

- rather than indexing using `[]` with a single number, you can use `[]` with a range to create a string slice containing particular bytes:
```rust
let hello = "Здравствуйте";

let s = &hello[0..4];
```
- `s` will be a `&str` that contains the first four bytes of the string (`s` will be `Зд` since these chars are two bytes each)

### Methods for Iterating Over Strings

- the best way to operate on pieces of strings is to be explicit about whether you want chars or bytes
- for individual scalar values, use the `chars` method
```rust
for c in "Зд".chars(){
	println!("{c}");
}
// prints
З
д
```

- the `bytes` method returns each raw byte
```rust
for b in "Зд".bytes() {
	println!("{b}");
}
// prints
208
151
208
180

```