Inserting `Strings` using pattern `${attribute}` works great with `Strings`. But `${}` can do . You can even run functions within it.

```nix
let 
	h = "Strings"
	v = 4;
in
{
	helloWorld = "${h} ${toString v} the win!";
}
```