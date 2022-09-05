# Fixed point arithmetic

**Fixed point arithmetic** is essentially taking the idea of a rational number and storing the top and bottom part - or just the top, if the bottom part can be made constant, which is usually the case.

## Formally

Formally, we have a rational number $N$:

$$N = \frac{A}{B}$$

<center>*$A/B$ can't be stored as a fraction!*</center>

And we eliminate the division to store the number in an integer:

$$BN = A$$

<center>*But of course, $A$ and $BN$ are integers!*</center>

Which gives us two numbers we can store as integers: $BN$ (or $A$) and $B$.

Keep in mind that since $A$ and $BN$ are equal, we only need to store one of them.

## Constant $B$

But it's kind of painful to store $B$ as a seprate integer. Plus, we don't really need to have a different division factor for each number; the same level of percision could really work for any value we want to store.

Instead of storing the base, we could instead decide on a constant base. 

This is, in fact, what most fixed point implementations use. For example, if a currecy is divided into `100` parts, then we would use `100` as the base and just store the amount times 100.

Or, if we wanted something that was faster than division, we could use exponents of 2 (e.g. $2^n$) to be able to use bit shifts during arithmetic operations, which will be useful once we learn how to do computations.

## Operations

For the operations, our goal is to find a number that can be stored as a fixed point $BP$, where $P = N * M$, the result of an operation $*$ on the rational numbers $N$ and $M$.

### Addition

Firstly, we want addition. Let's assume the base $B$ is the same, since that's what we will probably use most of the time.

We start with two numbers:

$$N = \frac{A}{B}$$
$$M = \frac{C}{B}$$

And add them together:

$$P = N + M$$

Then we can insert the rational number represented rationally.

$$P = N + M = \frac{A}{B} + \frac{C}{B} = \frac{A + C}{B}$$

So, we can see that if we multiply all sides by $B$:

$$BP = B(N + M) = BN + BM = A + C$$

Since $BP = BN + BM$, it seems that it is sufficent to just add the numbers!

```
Fixed add(Fixed x, Fixed y) {
	return x + y;
}
```

### Multiplication

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

### Division

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