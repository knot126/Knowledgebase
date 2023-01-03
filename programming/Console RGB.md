# Console RGB

24-bit RGB is supported by most consoles:

```c
printf("\x1b[38;2;%s;%s;%sm%s\x1b[0m", r, g, b, some_string);
```

* `\x1b` escape character
* `[` delimiter, idk why this char was chosen here.
* `38;2` code for rgb colour (very strange)
* `%s;%s;%s` the rgb colour
* `m` delimiter, again idk why this is it.
