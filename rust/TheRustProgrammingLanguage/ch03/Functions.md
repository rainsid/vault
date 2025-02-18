- *Function* is a reusable block of code that performs a specific task
```rust
fn main(){
   println!("Hello, world");
   another_function();
}

fn another_function(){
   println!("Another function");
}
```

# Parameters
- *Parameters* are special variables that are part of a function's signature
```rust 
fn main(){
   another_function(5);
}

fn another_function(x: i32){
   println!("The value of x is : {x}");
}
```

# Statements and Expressions
- *Statements* are instructions that perform some action and do not return a value
- *Expressions* evaluate to a resultant value
```rust
fn main(){
   let y = 6; // this is an example of a statement

   println!("The value of y is : {}", y);

// below is an expression
   let z  = {
	  let x = 3;
	  x + 1 
   }

   println!("The value of z is : {}", z);
}

/*!
this is the block that evaluates to 4
{
 let x = 3;
 x + 1; 
}
*/
```

# Functions with Return Values

- Functions can return values to the code that calls them
- we declare their type after an arrow (`->`)
- in Rust the return value of the function is synonymous with the value of the final expression in the block of the body of a function
- you can return early from a function by using the `return` keyword and specifying a value
```rust
fn five() -> i32 {
   5 
}

fn main(){
   let x = five();
   println!("The value of x is {}", x);
}
```

- another example
```rust
fn main(){
  let x = plus_one(5);
  println!("the value of x is {x}");
}

fn plus_one(x: i32) -> i32 {
   x + 1
}
```
- we don't put semicolon at the end of the line `x + 1`, changing it fro an expression to a statement we will get an error