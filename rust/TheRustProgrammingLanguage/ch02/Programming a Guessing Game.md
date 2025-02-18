## Processing a Guess
```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {guess}");
}
```

- bring *`io`* into scope
``` rust
use std::io;
```

- *`main`* function is the entry point of the program
```rust
fn main(){
```

---
## [[Storing Values with Variables]]
---

- *`String::new()`* - a function that returns a new instance of a *[[String]]*
-  the `::` syntax in `::new` line indicates the `new` is an associated function of the *String* type
- an *associated function* is a function that's implemented on a type

## Receiving User Input
- use *`stdin`* function from `io` module, which will allow us to handle user input
```rust
io::stdin().read_line(&mut guess);
```
- the `stdin` function returns an instance of `std::io::Stdin`, which is a type that represents a handle to the standard input for the terminal
- `read_line(&mut guess)` calls the `read_line` method on the standard input handle to get the input from the user
- the `&` indicates that this arg is a [[reference]], which gives you a way to let multiple parts of your code access one piece of data without needing to copy that data into memory multiple times

## Handling Potential Failure with Result
- `read_line` function returns a *Result* value
	- *Result* is an [[enumeration]] (enum), which is a type that can be in one of multiple possible states (we call them *variants*)
	- *Result*'s variants (states) are *ok* and *Err*
```rust
 .expect("Failed to read line");
```
- an instance of *Result* has an *expect* method

## Printing Values with *println!* Placeholders
```rust
    println!("You guessed: {guess}");
```
- `{}` - this set of curly brackets is a placeholder

---
## Generating a Secret Number
### Using a Crate to Get More Functionality
- Crate is a collection of Rust source code files
- we will use the *rand* crate to include random number functionality
- we need to modify *Cargo.toml* file to include rand crate as a dependency
```toml
[dependencies]
rand="0.8.5"
```

## Generating a Random Number
```rust
use std::io;
use rand::Rng;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100);

    println!("The secret number is: {secret_number}");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {guess}");
}
```

- the `Rng` defines methods that random number generators implement
- `rand::thread_rng` function gives us the particular random number generator we are going to use: one that is local to the current thread of execution and is seeded by the OS
- we then call `gen_range` method on the random number generator
	- this method is defined by the `Rng` trait that we brought into scope
	- this method takes a range of expression as an argument and generate a random number in that range
		- the range takes the form `start..=end` and is inclusive on the lower and upper bounds

## Comparing the Guess to the Secret Number
```rust
use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    // --snip--

    println!("You guessed: {guess}");

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```

- we add another type into the scope which is the `std::cmp::Ordering`
	- the `Ordering` type is another [[enumeration]] and has the variants `Less`, `Greater`, and `Equal`
- we use `cmp` method to compare two values
	- it takes a reference to whatever we want to compare with: here it's comparing `guess` to `secret_number`
	- it returns a variant of the `Ordering` enum
- we use [[match]] expression to decide what to do next based on which variant of `Ordering` was returned from the call to `cmp`

- we want to convert the `String` *guess* to a number type so we can compare it numerically to *secret_number*
```rust
    // --snip--

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

	// we add this line below
    let guess: u32 = guess.trim().parse().expect("Please type a number!");

    println!("You guessed: {guess}");

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
```
- Rust allows us to shadow the previous value of `guess`
- *Shadowing* lets us reuse `guess` var
- The `trim()` method on a *String* instance will eliminate any whitespace at the beginning and end
- the `parse()` method converts a string to another type
- the `:` in `let guess: u32` tells Rust we will annotate the variable's type


## Allowing Multiple Guesses with Looping
- `Loop` keyword creates an infinite loop
```rust
     // --snip--

    println!("The secret number is: {secret_number}");

    loop {
        println!("Please input your guess.");

        // --snip--

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => println!("You win!"),
        }
    }
}
```

### Quitting After a Correct Guess
- `Break` makes the program exit the loop
```rust
        // --snip--

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```

### Handling Invalid Input
- switch from `expect` call to a `match` expression
```rust 
        // --snip--

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("You guessed: {guess}");

        // --snip--
```
- if `parse` is able to successfully turn the string into a number it will return `ok` value that contains the resultant number otherwise match expression will return `Err(_)`
- `_` is a catchall value, we are saying that we want to match all `Err` values
