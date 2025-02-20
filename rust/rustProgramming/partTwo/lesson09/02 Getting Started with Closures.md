# Overview of Closures

- closures in Rust are the equivalent of lambdas in other programming languages
- a closure is similar to a nested function, but more flexible in several respects:
	- a closure can infer parameter/return types
	- a closure can capture external variables

## Syntax for Defining a Closure

- the syntax for defining a closure is similar (but simpler) to defining a nested function:
	- define parameters inside `||`
	- optionally specify parameter/return types
	- define the closure body inside `{}`
	
- you can assign a closure to a variable
	- then use the variable as if it were a function name, to invoke the closure