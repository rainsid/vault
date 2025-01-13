- Nix can also insert `Strings` with `${attribute}` where `attribute` is referenced from a let scope
```nix
let 
	h = "Hello"
in
{
	ex0 = "${h} World";
	ex1 = "${h + " " + "World"}";
	ex2 = ''${h + " " + "World"}'';
}
```