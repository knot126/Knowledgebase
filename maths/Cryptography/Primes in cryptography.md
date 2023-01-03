> Written with [StackEdit](https://stackedit.io/).

# Primes in cryptography

> Disclaimer: I am not exprienced, this is just some of my personal WIP learning notes.

Primes are very useful in cryptography becuase they can provide a function that is easy to compute and hard to reverse.

Essentially, it's hard - basically impossible - to find the prime factors of a large number (requires intense trial and error), but it is easy to make a number from its factors (which is just multiplication).

For example, say we have two random and large primes $P_0$ and $P_1$ that make a composite number $C$:

$C = P_0P_1$

Now, say you aren't given these primes:

$C = ab$

You can't easily find $a$ and $b$, the primes that make up the composite number.

Even though $C$ only has one prime factorisation, which *could* be found by brute force, we can be safe that it *probably won't* be in a reasonable amount of time if the factors are sufficently large enough.

## Primality tests

As part of the use of prime numbers, we need to be able to randomly generate primes. Sadly, there is currently [no fast function for $n$th primes](https://en.wikipedia.org/wiki/Formula_for_primes), so we can't just `NthPrime(SecureRandomNumber())`.

We need to resort to using division to test if a number that we randomly chose is prime. This is called *trial division*.

We might start with something very basic, like this:

```py
def is_prime(n):
		a = 2
		while (a != n):
				if (n % a == 0):
						return False
		return True
```

This will check that $n$ is not divisible for values of $a \in [2, n - 1]$, which comes from the definition of primality.

Of course, we're doing more work than we need to: we only have to check values of $a$ that are prime themselves. For example, a number divsible by $4$ will certianly be divisble by $2$ since $2$ is part of $4$'s prime factorisation itself ($4 = 2 \cdot 2$).

Now we've got:

```py
primes = [...]

def is_prime(n):
		for p in primes[0:NumberOfPrimesLessThan(n)]:
				if (n % p == 0):
						return False
		return True
```

We can also make one other observation...

If you had a number that was composite, $n = pq$, then we would have detected the lowest factor first, e.g. if $p < q$ then we would have found $p$ first because we are checking in ascending order.

The worst we need to handle is when $p = q$, since we would have detected if it was composite by that point.

> **Point of confusion**
> 
> I was originally confused why we are allowed to assume that there are two primes in the factorisation $n = pq$, when prime factorisations can have as many factors as you want.
> 
> It turns out this is the *worst case* that we need to work with. If there were any more prime factors, at least one factor would have been smaller than $\sqrt{n}$ and so we would already have ruled this number as composite.

Our final trial division turns out to be:

```py
primes = [...]

def is_prime(n):
		for p in primes[0:NumberOfPrimesLessThan(celi(sqrt(n)))]:
				if (n % p == 0):
						return False
		return True
```

Sadly, this is still not very good.
