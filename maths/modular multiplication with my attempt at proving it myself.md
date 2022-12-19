> Written with [StackEdit](https://stackedit.io/).

$(A \cdot B) \mod C = (A \mod C) \cdot (B \mod C) \mod C$

## my proof attempt

Lets use floors...

$x \mod y = x - y \lfloor x/y \rfloor$

Given
$ab \mod c = ab - c \lfloor ab/c \rfloor$
$a \mod c = a - c \lfloor a/c \rfloor$
$b \mod c = b - c \lfloor b/c \rfloor$

Let's try directly
$(a - c \lfloor  a/c \rfloor)(b - c \lfloor  b/c \rfloor)$
$a(b - c \lfloor  b/c \rfloor) - c\lfloor a/c \rfloor(b - c \lfloor  b/c \rfloor)$
$ab - ac \lfloor  b/c \rfloor - c\lfloor a/c \rfloor b + c\lfloor a/c \rfloor c \lfloor  b/c \rfloor$
$ab - ac \lfloor  b/c \rfloor - cb\lfloor a/c \rfloor + c^2\lfloor a/c \rfloor \lfloor  b/c \rfloor$
$ab + c^2\lfloor a/c \rfloor \lfloor  b/c \rfloor - ac \lfloor b/c \rfloor - cb\lfloor a/c \rfloor$
$ab + c(c\lfloor a/c \rfloor \lfloor  b/c \rfloor - a \lfloor b/c \rfloor - b\lfloor a/c \rfloor)$

It seems like that could work, if we can prove some kind of property of the floor function! Let's keep trying...

It seems like we need to show that
$-\lfloor ab/c \rfloor = c \lfloor a/c \rfloor \lfloor b/c \rfloor - a \lfloor b/c \rfloor - b \lfloor a/c \rfloor$

..... okay not tonight but MAYBE soon???

$c \lfloor a/c \rfloor \lfloor b/c \rfloor - \underbrace{a \lfloor b/c \rfloor}_{\text{excludes fractional part } E} - \underbrace{b \lfloor a/c \rfloor}_{\text{excludes fractional part } F}$
$c \lfloor a/c \rfloor \lfloor b/c \rfloor - a(b/c - E) - b(a/c - F)$
$c(b/c - E)(a/c - F) - a(b/c - E) - b(a/c - F)$
$c(b/c - E)(a/c - F) - ab/c - aE - ba/c - bF$
$c((b/c)(a/c - F) - E(a/c - F)) - ab/c - aE - ba/c - bF$
$c(ba/c^2 - bF/c - aE/c + FE) - ab/c - aE - ba/c - bF$
$ba/c - bF - aE + cFE - ab/c - aE - ba/c - bF$

It seems like we should be able to move things around from here...
$ba/c - 2bF - 2aE - 2ab/c + cFE$
$cFE + ba/c - 2bF - 2aE - 2ab/c$
$cFE - 2bF - 2aE - ab/c$
$cFE - 2(bF + aE) - ab/c$
$c^{-1}(c^2FE - 2c(bF + aE) - ab)$
$c^{-1}(FEc^2 - 2(bF + aE)c - ab)$
$c^{-1}FE(c^2 - 2(bF + aE)(FE)^{-1}c - ab(FE)^{-1})$
$c^{-1}FE(c^2 - 2(\frac{bF}{FE} + \frac{aE}{FE})c - ab(FE)^{-1})$
$c^{-1}FE(c^2 - 2(\frac{a}{F} + \frac{b}{E})c - \frac{ab}{FE})$

Define
$r = \frac{a}{F}$
$s = \frac{b}{E}$
$(a_1 + b_1)(a_1 + c_1) = a_1^2 + (a_1 + b_1)c_1 + b_1a_1$

[1] Continue with
$c^{-1}FE(c^2 - 2(r + s)c - rs)$

> this proof might not work actually... or i fucked it too hard X3

$c^{-1}FE(c^2 - 2(r + s)c + (r + s)^2 - (r + s)^2 - rs)$
$c^{-1}FE((c - (r + s))^2 - (r + s)^2 - rs)$
$c^{-1}FE((c - (r + s))^2 - (r + s)^2 - rs)$

$$\frac{FE((c - (r + s))^2 - (r + s)^2 - rs)}{c}$$

Remember: For everything to work out this just needs to simplify to $\lfloor ab/c \rfloor$ somehow

$$\frac{FE((c - ((\frac{a}{F}) + (\frac{b}{E})))^2 - ((\frac{a}{F}) + (\frac{b}{E}))^2 - (\frac{a}{F})(\frac{b}{E}))}{c}$$

$$\frac{FE(c - ((\frac{a}{F}) + (\frac{b}{E})))^2 - FE((\frac{a}{F}) + (\frac{b}{E}))^2 - FE(\frac{a}{F})(\frac{b}{E})}{c}$$

$$\frac{FE(c - ((\frac{a}{F}) + (\frac{b}{E})))^2 - FE((\frac{a}{F}) + (\frac{b}{E}))^2 - ab}{c}$$

$$\frac{FE(c - ((\frac{a}{F}) + (\frac{b}{E})))^2 - FE((\frac{a}{F}) + (\frac{b}{E}))^2 - ab}{c}$$

*sigh*

### trying by starting from [1]

$$c^{-1}FE(c^2 - 2(r + s)c - rs)$$

$$\frac{FE(c^2 - 2(r + s)c - rs)}{c}$$

$$\frac{FE(c^2 - 2((\frac{a}{F}) + (\frac{b}{E}))c - (\frac{a}{F})(\frac{b}{E}))}{c}$$

$$\frac{FE(c^2 - 2((\frac{a}{F}) + (\frac{b}{E}))c - (\frac{a}{F})(\frac{b}{E}))}{c}$$

this proof is fucked... 3':

### checking factoring quickly

$(da + b)(a + c)$
$da(a + c) + b(a + c)$
$(daa + dac) + (ba + bc)$
$(da^2 + dac) + (ba + bc)$
$da^2 + dac + ba + bc$
$da^2 + dac + bc + ba$
$da^2 + c(da + b) + ab$

## good proof

Show that $\Phi_0 = \Phi_1$ when
$\Phi_0 = (A \cdot B) \mod C$
$\Phi_1 = (A \mod C) \cdot (B \mod C) \mod C$
