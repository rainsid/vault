# Flow Control

## [[If-Test]]
- if-tests in rust are similar to most other languages:
```rust
let age = 58;
if age > 50 {
	println!("You are old");
}
```
- Note the ff points:
	- Test expression must be *bool*
	- No need for parentheses around test
	- Blocks must always be enclosed in {}

## If-Else-Test
- You can write an if-else test as follows:
```rust
let height = 1.68;

if height > 1.8{
	println!("You are tall");
} else {
	println!("You are not so tall");
}
```

## If-Else-If Test
- You can write an if-else-if as follows:
```rust
let swans_games = 500;

if swans_games > 300{
	println!("You are a loyal fan");
} else  if swans_games > 100 {
	println!("You are a discerning fan");
} else {
	println!("You are quite a new fan");
}
```

---
### Writing an If-Else Expression
- You can use if-else as an expression:
```rust
let msg = if age > 50 {"old"} else {"young"};

println!("You are {}", msg);
```
- This is similar to  *?:* in other languages

---
## Matching

^dc7c24

- Rust has a *match* keyword, which you can use to match:
	- [[Integers]]
	- [[Booleans]]
	- [[Enums]]
	- [[Arrays]]
	- [[Tuples]]
	- [[Structs]]
- You can match an expression against specific values:
```rust
let num = 100;

match num {
	100 => println!("A hundred"), //we call this "arm" in Rust. in other languages 
	200 => println!("Two hundred"), // that uses "switch", you'd call it a branch
	_ => println!("Something else")
}
```

- The branches are called *arms*
	 -  You can enclose arms in {}, if needed
- The arms must be exhaustive
	- you can use a catch-all (an underscore) to cater other values
	
### Matching Ranges
- You can match an expression against a range:
```rust
match num {
	25..=50  => println!("25 to 50"),
	51..=100 => println!("51 to 100"),
	_        => println!("Something else")
}
```
- the upper limit must be inclusive

### Matching Multiple Patterns
- You can specify multiple patterns, by using the | syntax:
```rust
match num {
	25 | 50 | 75 => println!("25, 50, or 75"),
	100 | 200    => println!("100 or 200"),
	_            => println!("Something else")
}
```

### Matching Conditions
- You can match against conditions:
```rust
match num {
	x if x < 50 => println!("Less than 50"),
	x if x == 75 => println!("75"),
	_            => println!("something else")
}
```

-  the conditions are called *match guards*

### Writing Match Expressions
- You can use match as an expression:
```rust 
let res = match num {
	x if x < 50 => "Less than 50",
	x if x == 75 => "75",
	_            => "something else"
};

println!("Result of match expression: {}", res);
```