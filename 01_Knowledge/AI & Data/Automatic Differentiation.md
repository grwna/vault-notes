Based on a *computational graph*.
Which are directed acyclic graphs where the nodes are variables and operations on those variables. Example:
$$z=x^2+3xy+1$$
Z will be the root and the leaf are all the unique variables and constants in the expressions. (Note: the empty nodes should actually have operators)
![[Pasted image 20260314232401.png|500]]

The nodes in this graph can be interpreted to represent composite functions which results in the next composite functions (or the root). Since they are functions, we can derivate each functions  once we have this graph.
The derivations are done recursively like so:
$$ \frac{\mathrm{d}}{\mathrm{d}x} f(g(x)) =\frac{\mathrm{d}}{\mathrm{d}g} f(g(x)) \cdot  \frac{\mathrm{d}}{\mathrm{d}x} g(x)$$
"To differentiate $f$ w.r.t to $x$, we must recursively derive $g$, then multiply the result with the derivative of $f$ w.r.t its argument ($g$)"