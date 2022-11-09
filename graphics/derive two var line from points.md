# Derive two variable line form from two points

Two variable line form (slope intercept): $y = rx + c$

Known points on the line: $A$, $B$

Defition of rate of change/slope: $r = \frac{\Delta y}{\Delta x}$

$$\Delta x = B_x - A_x$$

$$\Delta y = B_y - A_y$$

$$r = \frac{B_y - A_y}{B_x - A_x}$$

The following is also true of any $(x, y)$ on the line:

$$\Delta x = x - A_x$$

$$\Delta y = y - A_y$$

$$r = \frac{y - A_y}{x - A_x}$$

Then we can say that:

$$\frac{B_y - A_y}{B_x - A_x} = \frac{y - A_y}{x - A_x}$$

Multiply:

$$(B_y - A_y)(x - A_x) = (y - A_y)(B_x - A_x)$$

Expand:

$$x(B_y - A_y) - A_x(B_y - A_y) = y(B_x - A_x) - A_y(B_x - A_x)$$

$$x(B_y - A_y) - A_xB_y + A_xA_y = y(B_x - A_x) - A_yB_x + A_yA_x$$

Subtract the $A_xA_y$:

$$x(B_y - A_y) - A_xB_y = y(B_x - A_x) - A_yB_x$$

Add:

$$x(B_y - A_y) - A_xB_y + A_yB_x = y(B_x - A_x)$$

Divide:

$$x\frac{(B_y - A_y)}{(B_x - A_x)} - \frac{A_xB_y + A_yB_x}{(B_x - A_x)} = y$$

Make it look more obvious:

$$y = \frac{(B_y - A_y)}{(B_x - A_x)}x - \frac{A_xB_y + A_yB_x}{(B_x - A_x)}$$

And so:

$$y = \underbrace{\frac{(B_y - A_y)}{(B_x - A_x)}}_rx - \underbrace{\frac{A_xB_y + A_yB_x}{(B_x - A_x)}}_c$$
