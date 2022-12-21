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
