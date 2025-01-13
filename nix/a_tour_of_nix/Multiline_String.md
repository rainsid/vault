In Nix you are frequently using multiline `strings` to create text files using two qoutes, i.e. `''xxx''` in combination with attributes:
```nix
foo = ''
	foo: ${fooValue}
	bar: ${barValue}
'';
```
---

```nix

let 
	user = "mrNix";
	pass = "supersecretpass99";
	vip = true;
	vipString = if vip == true then ''vip: "true" '' else "";
in
{
	ex0 = ''
	${user}
		password: ${pass}
		${vipString}
	'';
}
```
