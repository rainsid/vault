# Let Expression
- the `let` expression is composed of
	- `let <bindings> in <body>`
- the bindings are a series of definitions separated by semi-colons

```nix
let 
	h = "Hello";
	s = " ";
	w = " ";
in {
	helloWorld =  h + s + w;
}
```