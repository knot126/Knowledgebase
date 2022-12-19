> note: you need to load this in stack edit otherwise it doesn't look good

Given:
$a, b \in \mathbb{Z}$

Note that:
$a / b = w + f$, for $w \in \mathbb{Z}$ and $f \in [0, 1)$
$a = bw + bf$

Define:
$q = w$
$p = bf$

$a = \overbrace{bq}^{\mathbb{Z} \cdot \mathbb{Z} \rightarrow \mathbb{Z}} + p$

What about $p$?

We know that:
$f = a/b - \lfloor a/b \rfloor$
$bf = a - b \lfloor a/b \rfloor$

The floor must still result in a fraction $n/b$:
$n/b = \lfloor a/b \rfloor$, for $n \in \mathbb{Z}$
$n = b \lfloor a/b \rfloor$
Since $n = b \lfloor a/b \rfloor$ and $n \in \mathbb{Z}$, this means $b \lfloor a / b \rfloor \in \mathbb{Z}$

**Another way to think about this...**

Imagine that $a/b = c/b + d/b$, where $c, d \in \mathbb{Z}$ and that $c / b =\lfloor a / b \rfloor$
$a/b - c/b = d/b$
$b(a/b - c/b) = b(d/b)$
$\underbrace{a - c}_{\mathbb{Z} - \mathbb{Z} \rightarrow \mathbb{Z}} = d$

You can see that $d \in \mathbb{Z}$

but how the fuck can we explain that b * floor(a/b) must be an integer definitively???

like i understand that but is there a more formal way to think about this too?

maybe the solution is a visual proof, probably to be saved for tomorrow...
