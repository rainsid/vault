# If Expressions
- allows you to branch your code depending on conditions
```rust
fn main(){
   let number = 3;

   if number < 5 {
	  println!("condition was true"); 
   } else {
	  println!("condition was false"); 
   }
}
```
- the condition must be a `bool`

## Handlinng Multiple Conditions with `else if`

```rust
fn main(){
	let number = 6;
	if number % 4 == 0 {
		println!("number is divisible by 4");
	} else if number % 3 == 0 {
		println!("number is divisible by 3");
	} else if number % 2 == 0 {
		println!("number is divisible by 2");
	} else {
		println!("number is not divisible by 2, 3 or 4");
	}
}
```
- the program has four possible paths it can take

## Using `if` in a `let` Statement
- because `if` is an expression, we can use it on the right side of a `let` statement to assign the outcome to a variable
```rust
fn main(){
	let condition = true;
	let number = if condition { 5 } else { 6 };
	println!("The value of number is: {number}");
}
```
- results of both the `if` arm and the `else` arm must be of the same type
- we'll get an error if they are mismatched
- Rust needs to know at compile time what type the var `number` is


---

# Repetition with Loops
## Repeating Code with `loop`
- `loop` keyword tells rust to execute a block of code over and over again forever or until you explicitly tell it to stop
```rust
fn main(){
	loop{
		println!("again!");	
	}
}
```

## Returning Values from Loops
```rust
fn main(){
	let mut counter = 0;
	let result = loop{
		counter += 1;

		if counter  == 10 {
			break counter * 2;	
		}
	};
	println!("The result is {result}");
}
```

## Loop Labels to Disambiguate Between Multiple Loops

- you can optionally specify a *loop label* on a loop that you can then use with `break` or `continue` specify that those keywords apply to the labeled loop instead of the innermost loop
```rust
fn main (){
 let mut count = 0;
    'counting_up: loop {
        println!("count = {}", count);
        let mut remaining = 10;

        loop {
            println!("remaining = {}", remaining);
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }

    println!("End count = {}", count);
}
```

## Conditional Loops with`while`
```rust
fn main(){
	let mut number = 3;

	while number != 0 {
		println!("{}", number);	

		number -= 1;
	}

	println!("LIFTOFF!");
}
```

## Looping Through a Collection with `for`
```rust
fn main(){
	let a = [10,20,30,40,50];

	for element in a{
		println!("the value is: {element}");
	}
}
```

- we can use `Range` in a for loop
```rust
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```