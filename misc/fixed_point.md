# Fixed point arithmetic

> TODO: I do reference the base ($B$) as being variable a lot, even though fixed point rarely has a variable base. This should be refactored to consider the base being a constant value.

**Fixed point arithmetic** is essentially taking the idea of a rational number and the idea of multiplication undoing division in order to store rational numbers in integer data types.

## Formally

Formally, we have a rational number $N$, with $A$ being divided by some base $B$:

$$N = \frac{A}{B}$$

<center>*$A/B$ can't be stored as an integer!*</center>

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

So, we start with the numbers stored as fixed point values:

$$X = BN$$
$$Y = BM$$

Then we find their product as normal:

$$X \cdot Y = B^2 NM$$

And now, we want to find the product represented as a fixed point number, which should only involve one $B$. So, we can divide by $B$ to get:

$$\frac{X \cdot Y}{B} = BNM$$

So, our product is the fixed point number $X$ times the fixed point number $Y$ divided by $B$ to account for the squaring of $B$ that happens when we multiply the two.

----

Do note that you can also rewrite this as:

$$\frac{X \cdot Y}{B \cdot B} = NM$$

Which is representitve of the product of the numbers we are storing, $N \cdot M$, and how they are stored, by being multiplied by $B$, giving us the value $BNM$ used to store the result.
