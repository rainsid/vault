- `match` allows you to compare a value against a series of patterns and then execute code based on which pattern matches

```rust
enum Coin {
	Penny,
	Nickel,
	Dime,
	Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
	match coin {
		Coin::Penny => 1,	
		Coin::Nickel => 5,	
		Coin::Dime => 10,	
		Coin::Quarter => 25,	
	}
}
```

- the condition in `match coin` can be of any type (with `if`, the condition needs to evaluate to a Boolean value)
- `match` arms has two parts: pattern and some code
	- the first arm has a pattern that is the value `Coin::Penny` and then the `=>` operator that separates the pattern and the code to run in this case the value `1`
- when match expression executes, it compares the resultant value against the pattern of each arm, in order
- if pattern matches the value, the code associated with that pattern is executed
- if the pattern does not match the value, execution continues to the next arm
- we can use curly brackets if we want to run multiple lines of code in a match arm
```rust
fn value_in_cents(coin: Coin) -> u8 {
	match coin {
		Coin::Penny => {
			pirntln!("Lucky penny!"); 
			1
		}
		Coin::Nickel => 5, 
		Coin::Dime => 5, 
		Coin::Nickel => 5, 
	}
}
```

## Patterns That Bind to Values

```rust
#[derive(Debug)] 
enum UsState {
	Alabama,
	Alaska,
	// --snip--
}

enum Coin {
	Penny,
	Nickel,
	Dime,
	Quarter(UsState),
}
```
- From 1999 through 2008, the United States minted quarters with different designs for each of the 50 states on one side. No other coins got state designs, so only quarters have this extra value. We can add this information to our `enum` by changing the `Quarter` variant to include a `UsState` value stored inside it
```rust
fn value_in_cents(coin: Coin) -> u8 {
	match coin {
		Coin::Penny => 1,	
		Coin::Nickel => 5,	
		Coin::Dime=> 10,	
		Coin::Quarter(state) => {
			println!("State quarter from {state: ?}!");
			25
		}	
	}
}
```
- we add a variable called state to the pattern that matches the value of the variant `Coin::Quarter`
- when a `Coin:Quarter` matches, the `state` variable will bind to the value of the quarter's state

---

## Matching with `Option<T>` 

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
	match x {
		None => None,
		Some(i) => Some(i + 1),	
	}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
}
```
- `plus_one` takes an `Option<i32>`, if there is a value inside, adds 1 to that value, if there is not a value inside, the function returns `None` value and not attempt to perform any operations

---

## Matches are Exhaustive
```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
	match x {
		Some(i) => Some(i + 1),	
	}
}
```
- we did not handle the `None` case so we will get an error if we try to compile
- Rust knows that we did not cover every possible case

---

## Catch-all Patterns and the `_` Placeholder

```rust
let dice_roll = 9;
match dice_roll {
	3 => add_fancy_hat(),
	7 => remove_fancy_hat(),
	other => move_player(other),
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn move_player(num_spaces: u8) {}
```
- the last pattern will match all values not specifically listed
- we have to put the catch-all arm last because the patterns are evaluated in order

- Rust `_` is a special patter that matches any value and does not bind to that value
```rust
let dice_roll = 9;
match dice_roll {
	3 => add_fancy_hat(),
	7 => remove_fancy_hat(),
	_ => reroll(),
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn reroll() {}
```

- if we want the game so that nothing else happens on your turn if you roll anything other that a `3` or `7`
- we can express that by using the unit value `()` (the empty tuple type)
```rust
let dice_roll = 9;
match dice_roll {
	3 => add_fancy_hat(),
	7 => remove_fancy_hat(),
	_ => (),
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
```
- we are telling Rust explicitly that we are not going to use any other value that does not match a pattern in an earlier arm, and we don't want to run any code