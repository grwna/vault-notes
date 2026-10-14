# Keywords
- Rings
- Divisibility
- GCD

# Number Theory
Number theory is the study of the integers. The set of integers is denoted by $\mathbb{Z}$. The set of integers with their addition and multiplication rules are an example of a [[Rings, Quotients, Polynomials, and Finite Fields|ring]]. If we add, subtract, multiply integers with integers, we always get integers back. **However**, this might not work for division ($\frac{3}{2}$). This leads to the concept of **divisibility**

$b$ divides $a$ if there is an integer $c$ such that: $$a=bc$$We write $b\mid a$ to indicate it. Otherwise, we indicate with $b \nmid a$.

**Proposition 1.4**
Let $a,b,c\in \mathbb{Z}$
(a) $\text{if } a\mid b \text{ and } b \mid c \text{, then } a\mid c$
(b) $\text{if } a\mid b \text{ and } b \mid a \text{, then } a=\pm b$
(c) $\text{if } a\mid b \text{ and } a \mid c \text{, then } a\mid (b+c) \text{ and } a\mid (b-c)$

# Greatest Common Divisor
Largest positive integer $d$ such that $d \mid a$ and $d \mid b$, Denoted $\text{gcd}(a,b) = d$. The humble GCD has many applications. The most efficient way to calcualte GCD is to take advantage of the fact that:
$$\text{gcd}(a,b)=\text{gcd}(b,r)$$
Where $$a=b\cdot q+r$$
Eventually, $r$ will be zero, where the final $b$ is the gcd (or the final non-zero reminder). This is called the **Eucledian Algorithm**.

**Extended Euclidean Algorithm**
$$au+bv=\text{gcd}(a,b)$$

