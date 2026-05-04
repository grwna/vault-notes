Continued fractions help us find good approximations for real life constants.

# Introduction
## Euclid's GCD
[[Modular Arithmetic#Euclid's GCD|Euclid's GCd]]

Continued fractions can be seen in the calculations of GCD, say we need to find $GCD(43,19)$, we would do:
$$\begin{align}
	43&=2\times 19+5 \\
	19&=3\times 5+4 \\
	5&=1\times 4+1 \\
	4&=4\times 1 + 0
\end{align}$$
Notice the *quotients* of at each step. If we were to write $\frac{43}{19}$, we will have a "recursive" fraction effect. (Try to calculate the equation $\frac{43}{19}$)

$$\frac{43}{19}=2+\frac{1}{3+\frac{1}{1}}$$