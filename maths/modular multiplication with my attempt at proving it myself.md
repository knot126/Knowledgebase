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

## good proof

Show that $\Phi_0 = \Phi_1$ when
$\Phi_0 = (A \cdot B) \mod C$
$\Phi_1 = (A \mod C) \cdot (B \mod C) \mod C$
