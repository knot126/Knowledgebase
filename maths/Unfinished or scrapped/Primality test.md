> Written with [StackEdit](https://stackedit.io/).

# Primality tests

The main idea of the primality test is that it tests if a number is prime ... maybe that was obvious from the name.

## An initial test

The most obvious way to check if a number is prime is actually to check if it is not composite.

Put simpily, we check each possible factor that could divide $n$ ($2$, $3$, $4$, $5$ ... $n - 1$) to determine weather it is composite or prime. If we find one that divides evenly, we know that $n$ is composite!

## Avoiding repetition

One problem with our initial test is that it actually includes fators that we have already checked. For example, $4$ factors to $2 \cdot 2$, so if we've checked $2$ then we've also checked $2 \cdot 2 = 4$ or any number that has a prime factorisation with $2$ in it.

To do this, we can divide only by numbers that don't have any factors we've already tested.

Our sequence to test against is now $2, 3, 5, 7, 11, 13 ... (n-1)$, or the prime numbers before the number we want to test as prime.

## Better boundaries

Of course, we still need to test a lot of numbers, up to $n-1$! We can do a bit better.

Let's think about the largest possible prime factorisation for some number $n$. Call the largest prime that divides $n$ to be $p_0$.

$n = p_0m_0$, where $p_0$ is the largest prime factor of $n$


$m_0$ must also have a largest prime factor itself:

$n = p_0\underbrace{m_0}_{p_1m_1}$
$n = p_0p_1m_1$, with $p_0 \ge p_1$

And this is the same for $m_1$:

$n = p_0p_1p_2m_2$, with $p_0 \ge p_1 \ge p_2$

And so on, until $m_x = 1$ and we can stop:

$n = p_0p_1p_2 \cdots p_{x-1}$, with $p_0 \ge p_1 \ge p_2 \ge \cdots \ge p_{x-1}$

For a moment, let's just a assume that there are two primes in the factoristation:

$n = p_0p_1$, with $p_0 \ge p_1$

As you can see, the worst possible case of the size of $n$ is that $p_0 = p_1$:

$n = p_0p_1$, with $p_0 = p_1$

$n = p_0^2$

$\sqrt{n} = p_0$

So if we have two 
