# Old fixed point explainations

**IMPORTANT**: This is an older explaination of multiplication that's not as well written, but it might help for some people, so I will leave it here.

## Old/alternate explaination of multiplication

Now, what about multiplication? We want to find what we do to get $B(NM)$, which is the numbers multiplied and represented as a fixed point integer.

$$N = \frac{A}{B}$$
$$M = \frac{C}{B}$$

Multiply, of course:

$$P = N \cdot M = \frac{A}{B} \cdot \frac{C}{B} = \frac{AC}{B^2}$$

Now we can multiply by $B$ to get $BNM$:

$$BP = BNM = \frac{AC}{B}$$

So, we can multiply the values, then divide by the base $B$:

```c
Fixed multiply(Fixed x, Fixed y) {
	return (x * y) / b;
	// Or if your base is a power of two: (x * y) >> n, where B = 2^n.
}
```

## Old explaination of division

When handling division, we still start with simple facts:

$$N = \frac{A}{B}$$
$$M = \frac{C}{B}$$

Where we can then define the problem:

$$P = \frac{N}{M} = \frac{\frac{A}{B}}{\frac{C}{B}}$$

And do some nice algebra to eliminate the base:

$$\frac{\frac{A}{B}}{\frac{C}{B}} = \frac{B^{-1}A}{B^{-1}C} = \frac{A}{C}$$

Where we can finally find:

$$BP = B(\frac{N}{M}) = B(\frac{A}{C})$$

And therefore:

```c
Fixed divide(Fixed x, Fixed y) {
	return (x / y) * b;
	// Or if your base is a power of two: (x * y) << n, where B = 2^n.
}
```