> Written with [StackEdit](https://stackedit.io/).

$(A \cdot B) \mod C = (A \mod C) \cdot (B \mod C) \mod C$

## Intuition

Essentially, mutliplication is scaling the rope or clock hand by some factor, which is also subject to the modulus. For example, multiplying by two 

## Proof

Show that $\Phi_0 = \Phi_1$ when
$\Phi_0 = (A \cdot B) \mod C$
$\Phi_1 = (A \mod C) \cdot (B \mod C) \mod C$

We can write $A$ and $B$ as
$A = CP_A + Q_A$
$B = CP_B + Q_B$

And now, we split this proof into two (or three) parts.

### Part 1: Show that $\Phi_0 = Q_A \cdot Q_B \mod C$

$\Phi_0 = (CP_A + Q_A) \cdot (CP_B + Q_B) \mod C$
$\Phi_0 = (CP_A + Q_A) \cdot (CP_B + Q_B) \mod C$
$\Phi_0 = (CP_ACP_B + CP_AQ_B + Q_ACP_B + Q_AQ_B) \mod C$
$\Phi_0 = (CP_ACP_B \mod C + CP_AQ_B \mod C + Q_ACP_B \mod C + Q_AQ_B \mod C) \mod C$

It is easy to see that $cn \mod c = 0$ since $cn$ is always a multipule of $c$ and therefore has a remainder of zero, which by defition is what modulus gives us. Knowing this, we can write:

$\Phi_0 = (Q_A \cdot Q_B \mod C) \mod C$

And of course $(n \mod c) \mod c = n \mod c$ so:

$\Phi_0 = Q_A \cdot Q_B \mod C$

### Part 2: Show that $\Phi_1 = Q_A \cdot Q_B \mod C$

$\Phi_1 = (A \mod C) \cdot (B \mod C) \mod C$
$\Phi_1 = ((CP_A + Q_A) \mod C) \cdot ((CP_B + Q_B) \mod C) \mod C$
$\Phi_1 = ((CP_A \mod C + Q_A \mod C) \mod C) \cdot ((CP_B \mod C + Q_B \mod C) \mod C) \mod C$

It is easy to see that $cn \mod c = 0$ since $cn$ is always a multipule of $c$ and therefore has a remainder of zero, which by defition is what modulus gives us. Knowing this, we can write:

$\Phi_1 = ((Q_A \mod C) \mod C) \cdot ((Q_B \mod C) \mod C) \mod C$

And of course $(n \mod c) \mod c = n \mod c$ so:

$\Phi_1 = (Q_A \mod C) \cdot (Q_B \mod C) \mod C$

And since $Q_A$ and $Q_B$ are already $\mod C$ becuase they are remainders, we can write:

$\Phi_1 = Q_A \cdot Q_B \mod C$

### Part 3

Now, let's look at our final results:

* $\Phi_0 = Q_A \cdot Q_B \mod C$
* $\Phi_1 = Q_A \cdot Q_B \mod C$

So, we can say that $\Phi_0 = \Phi_1$!

And that is it, we have proven this property of modulus.
