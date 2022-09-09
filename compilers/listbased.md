# List-based programming language

This document covers ideas for a list based, expression-only programming language.

## Lists and Values

Lists are lists of values, as in other languages. Values can be strings, integers, numbers or other lists.

```
[5, 2, 6, "test", ("another", "list")]
```

Simple expressions can also be used instead of values:

```
[5 * 2, 17 - 23, 88 + 1, "First" .. " Last"]
```

Values can have names. If a value has a name, it can be accessed within the array later by calling its name:

```
[string1 = "abc", string2 = "def", string1 .. string2]
```

If a value has a name, it still emits the value it is being assigned to, and it still counts as an index in the list:

```
{
	abc = 300, -- emits 300
	def = $:0; -- access the first 
}
```

Note that lists can use any opening/closing pairs and intermix them, as well as using either `,` or `;` to septate values and intermixing them:

```
{
	{6, 3, 5, 1, 5, 2, 5},
	[69, 421);
	<5, 21, 53>;
}
```

A list can have its indices accessed with a colon then the index number:

```
{
	list = [1, 2, 3, 4, 5];
	list:3; -- emits 3
}
```

Lists are always indexed from zero.

A list can access itself by using the `$` or `§`:

```
{
	§:0; -- refers to itself
	130;
	$:1; -- refers to value 130 in the list
}
```

## Comments

Comments are like SQL, Lua and other languages that use `--` to start a comment. They run until the end of the line.

```
-- This is a comment
```

## Programs

A full program, of course, is a list of expressions that need to be evaluated:

```
[
	5 * 7 * 2, -- expression 1
	6 + 2 * 5, -- expression 2
]
```

## Functions

A function is a generic list of instructions that are applied to a generic list of named arguments.

They take some named arguments, and eventually emit a value, probably based on those arguments:

```
{
	-- function to add two numbers
	add = (a, b) { emit a + b };
	
	-- the result of the addition of 5 and 2
	result1 = add(5, 2); -- emits 7
	
	-- function to find length of side c of a triangle
	findc = (a, b) { emit sqrt(a * a + b * b); };
	
	-- the result of finding side c for lengths 3 and 4
	result2 = findc(3, 4); -- emits 5
	
	-- display the results using 'print'
	print("5 + 2 = ", result1);
	print("Pyth(3, 4) = ", result2);
}
```

If you could not tell, a function is called by referencing its value and giving it a list of arguments:

```
{
	myFunc = (varg)(emit print("hi, ", varg));
	
	$:0("Ruff"); -- call the function from an index
	myFunc("Chet"); -- call the function given the name
	
	(a, b){emit a + b}(5, 3); -- call the function right after defining it
}
```

Syntactically, a function is just two lists smashed together and is itself an evaluate-able value:

```
Function  = List List
```

If a function does not emit a value, all of its resulting values are returned as a list:

```
{
	nonEmittingFunction = (a, b, c) {
		a + b;
		c * a + b;
		b + c;
		b * b * c
	};
	
	list = nonEmittingFunction(5, 3, 7);
}
```

An implementation might decide that function that do not emit a value will run all of their tasks at once:

```
{
	myFunc = ()(print("1"), print("2"));
}
```

## Control Flow

All conditional flow is done using the C-like `?:` operator:

```
{
	user = input("Enter a value: ", input:ANY_TYPE);
	(true) ? print("true") : print("false");
}
```
