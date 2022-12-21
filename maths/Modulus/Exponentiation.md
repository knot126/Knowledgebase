> Written with [StackEdit](https://stackedit.io/).

# Modular exponentiation

$a^b \mod c = (a \mod c)^b \mod c$

## Proof

Try to find that $\Phi_0 = \Phi_1$, when:

$\Phi_0 = a^b \mod c$
$\Phi_1 = (a \mod c)^b \mod c$

### The full proof

$\Phi_0 = \underbrace{aaa \cdots a}_{b \text{ times}} \mod c$

$\Phi_0 = \underbrace{(a \mod c) \cdot (a \mod c) \cdot (a \mod c) \cdots (a \mod c)}_{b \text{ times}} \mod c$

$\Phi_0 = (a \mod c)^b \mod c$

Therefore $\Phi_0 = \Phi_1$.

## Splitting into parts

$R = x^e \mod a = x^{b+c} \mod a = x^bx^c \mod a$
$R = (x^b)(x^c) \mod a$
$R = ((x \mod a)^b \mod a)((x \mod a)^c \mod a) \mod a$
$\color{grey}R = (x \mod a)^b(x \mod a)^c \mod a$
$\color{grey}R = (x \mod a)^{b+c} \mod a$

## Faster algorithms

We can use multiplication rules to make things faster for powers of two:

$n_0 = a^{1} \mod c$
$n_1 = a^{2} \mod c = (n_0 \mod c) \cdot (n_0 \mod c) \mod c$
$n_2 = a^{4} \mod c = (n_1 \mod c) \cdot (n_1 \mod c) \mod c$
$n_3 = a^{8} \mod c = (n_2 \mod c) \cdot (n_2 \mod c) \mod c$
$$\vdots$$

$n_p = a^{2^{p}} \mod c = (n_{p-1} \mod c) \cdot (n_{p-1} \mod c) \mod c$

We can also break any exponent into powers of two:

$r = a^{26} \mod c$

$26 = 1 \cdot 2^4 + 1 \cdot 2^3 + 0 \cdot 2^2 + 1 \cdot 2^1 + 0 \cdot 2^0 = (11010)_2$

$r = a^{16+8+2} \mod c$

$r = a^{16}a^8a^2 \mod c$

$r = (a^{16} \mod c)(a^8 \mod c)(a^2 \mod c) \mod c$

So now we can do any exponent as powers of two. :)
