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

$x^e \mod c = x^{b+c} \mod c = x^bx^c \mod c$
