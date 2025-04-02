```rust
enum Result<T, E> {
	Ok(T),
	Err(E),
}
```
- the `T` and `E` are generic type params
	- `T` represents the type of the value that will be returned in a success case within the `Ok` variant
	- `E` represents the type of the error that will be returned in a failure case within the `Err` variant

```rust
use std::fs::File;

fn main(){
	let greeting_file_result = File::open("hello.txt");
}
```
- the return type of `File::open` is a `Result<T, E>`
- the generic param `T` has been filled in by the implementation of `File::open` with the type of the success value, `std::fs::File`
- the type of `E` used in the error values is `std::io::Error`

```rust
use std::fs::File;

fn main(){
	let greeting_file_result = File::open("hello.txt");

	let greeting_file = match greeting_file_result {
		Ok(file) => file,
		Err(error) => {panic!("Problem opening the file: {error:?}")},	
	};
}
```
- when the result is `Ok`, this code will return the inner `file` value out of the `Ok` variant, and we then assign that file handle value to the variable `greeting_file`
- the other arm of the `match` handles the case where we get an `Err` value from `File::open` 


--------

# Matching on Different Errors

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main(){
	let greeting_file_result = File::open("hello.txt");

	let greeting_file = match greeting_file_result {
		Ok(file) => file,
		Err(error) => match error.kind() {
			ErrorKind::NotFound => match File::create("hello.txt") {
				Ok(fc) => fc,
				Err(e) => panic!("Problem creating the file: {e:?}"),
			},
			other_error => {
				panic!("Problem opening the file: {other_error:?}");	
			}	
		},	
	};
}
```
- the type of value that `File::open` returns inside the `Err` variant is `io::Error` which is a struct provided by the standard lib
	- this struct has a method `kind` that we can call to get an `io::ErrorKind` value
	- the `io::ErrorKind` is provided by the standard lib and has variants representing the different kinds of errors that might result from an `io` operation

## Alternatives to Using `match` with `Result<T, E>`

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main(){
	let greeting_file = File::open("hello.txt").unwrap_or_else(|error|{
		if error.kind() == ErrorKind::NotFound {
			File::create("hello.txt").unwrap_or_else(|error| {
				panic!("Problem creating the file {error:?}");	
			})	
		} else {
			panic!("Problem opening the file {error:?}");	
		}	
	});
}
```
- here we use a *closure* and the `unwrap_or_else` method


-------

## Shortcuts for Panic on Error: unwrap and expect

- the `unwrap` method is a shortcut method implemented just like the `match` expression
```rust
use std::fs::File;

fn main(){
	let greeting_file = File::open("hello.txt").unwrap();
}
```
- if we run this code without a *hello.txt* file, we'll see an error message fro the `panic!` call that the `unwrap` method makes

```rust
use std::fs::File;

fn main(){
	let greeting_file = File::open("hello.txt")
		.expect("hello.txt should be included in this project");
}
```
- the `expect` method lets us also choose the `panic!` error message
- using `expect` instead of `unwrap` and providing good error messages can convey intent and make tracking down the source of a panic easier
- the error message used by `expect` in its call to `panic!` will be the param that we pass to `expect`

-----

## Propagating Errors

- when a function's implementation calls something that might fail, instead of handling the error within the function itself you can return the error to the calling code so that it can decide what to do
- *propagating* the error gives more control to the calling code, where there might be more info or logic that dictates how the error should be handled then what you have available in the context of your code

```rust
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
	let username_file_result = File::open("hello.txt");

	let mut username_file = match username_file_result {
		Ok(file) => file,
		Err(e) => return Err(e),	
	};

	let mut username = String::new();

	match username_file.read_to_string(&mut username){
		Ok(_) => Ok(username),
		Err(e) => Err(e),	
	}
}
```

### A Shortcut for Propagating Errors: the `?` Operator

```rust
use std::fs::File;
use sdt::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error>{
	let mut username_file = File::open("hello.txt")?;
	let mut username = String::new();
	username_file.read_to_string(&mut username)?;
	Ok(username)
}
```
- the `?` placed after a `Result` value is defined to work in almost the same way as the `match` expression
- if the value of the `Result` is `Ok`, the value inside the `Ok` will be returned from the expression and the program will continue
- if the value is an `Err`, the `Err` will be returned from the whole function as if we had used the `return` keyword so the error value gets propagated to the calling code

#### Chaining Method Calls

- we can even shorten the code by method chaining 
```rust
use std::fs::File;
use sdt::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
	let mut username = String::new();

	File::open("hello.txt")?.read_to_string(&mut username)?;

	Ok(username)
}
```
- we have chained the call to `read_to_string` directly onto the result of `File::open("hello.txt")?`

- we can make the code even shorter than the last one
```rust
use std::fs;
use std::io;

fn read_username_from_file() -> Result<String, io::Error> {
	fs::read_to_string("hello.txt");
}
```
- reading a file into a string is fairly common operation, so the standard lib provides the convenient `fs::read_to_string` function that opens the file, create a new `String`, read the contents of the file, puts the contents into the `String`, and returns it

-------
### Where The `?` Operator Can be Used

- the `?` operator can be used in functions whose return type is compatible with the value the `?` is used on
- this is because the `?` operator is defined to perform an early return of a value cut of the function, in the same manner as the `match` expression we defined
- the `match` was using a `Result` value, and the early return arm returned an `Err(e)` value
- the return type of the function has to be a Result so that it's compatible with this `return`

```rust
use std::fs::File;

fn main() {
	let greeting_file = File::open("hello.txt");
}
```
- this code will throw an error because `?` operator follows the `Result` value returned by `File::open`, but this `main` function has the return type of `()`
- we have two choices to fix this error:
	- change the return type of the function to be compatible with the value you are using `?` operator on as long as you have no restrictions preventing that
	- use a `match` expression or one of the `Result<T, E>` methods to handle the `Result<T, E>` in whatever way is appropriate

```rust
fn last_char_of_first_line(text: &str) -> Option<char> {
	text.lines().next()?.chars().last()
}
```
- the behavior of the `?` operator when called on an `Option<T>` is similar to its behavior when called on a `Result<T, E>`
	- if the value is `None`, the `None` will be returned early from the function at that point
	- if the value is `Some`, the value inside the `Some` is the resultant value of the expression, and the function continues

```rust
use std::error::Error;
use std::fs::File;

fn main() -> Result<(), Box<dyn Error>> {
	let greeting_file = File::open("hello.txt");

	Ok(())
}
```
- `main` can also return a `Result<(), E>` 
- `Box<dyn Error>` means “any kind of error”
- `main` will exit wit a value of `0` if it returns `Ok(())`
