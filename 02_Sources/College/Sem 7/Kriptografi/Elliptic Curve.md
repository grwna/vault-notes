# Basis
## Math
**Groups**
- Consists of:
	- Set G
	- Binary operation *
- Denoted with $<\text{set, op}>$
- Have properties:
	- Closure
	- Associative
	- Has a neutral element
	- Has an inverse element
	- If it has Commutative, it becomes an **abelian** group
- Since abelian groups are commutative, this allows it to be the foundation of some cryptographic schemes.

**Field**
- Consists of:
	- Set F
	- Binary operation + and $\cdot$ 
- Have Properties:
	- $<F,+>$ is an abelian group
	- $<F-{0},\cdot >$ is an abelian group
	- $\cdot$ and + are distributive

**Finite Field**
- Elements are finite, with element count written as $n$ ($F_{n}$)
- Prime finite fields ($F_{p}$, with $p$ prime), using $p$ as operation's modulus

**Galois Field**
- Finite fields with $p^m$ elements, with $p$ prime and $m\geq 1$
- Denoted as $GF(p^m)$
- if $p=2$, it is called binary finite fields, with $m$ denoting the length of the binary string
- In this way, binaries can be represented as polynomials, and when two binary polynomials are added, the results are the same as XOR.
- Other concepts:
	- Irreducible polynomials

# ECC Algorithm
## Theory
- Elliptic curve: $y^2=x^3+ax+b$
- $4a^3+27b^2\neq0$
- The curve form a group (abelian) with the addition operator
- The addition operator is specially defined below.
- Properties:
	- Inverse: $-P$
	- Neutral: $\mathcal{O}$ (point at infinity)
- Elliptic curves are vertically symmetrical

**Addition**
- Addition of point $P$ and $Q$ is $R$, which is the mirror of $-R$. 
- $-R$ is the 3rd intersection of the line that also intersects $P$ and $Q$ 
- Quick formulas:
	- Gradient: $m=\frac{y_{p}-y_{q}}{x_{p}-x_{q}}$
	- $x_{r}=m^2-x_{p}-x_{q}$
	- $y_{r}=m(x_{p}-x_{r})-y_{p}$

**Subtraction**
- $P-Q=P+(-Q)$

**Multiplication**
- Points can only multiplied by integer scalar
- Multiplication of a point $P$ with a scalar $x$ is defined by doing addition of point $P$, $x$ amount of times
- Gradient for multiplication is a derivative, with tangent slope:
	- $m=\frac{dy}{dx}=\frac{3x_{p}^2+a}{2y_{p}}$

**Point Iteration**
- $P^k=kP$
- The exact same as multiplication
- if $k=2$, it is called point doubling

## Cipher Basis
**ECDLP**
- $kP=Q$, is easy.
- Given $P, Q$, find $k$
	- This is difficult and is the basis for cipher safety
- This is called the elliptic curve discrete logarithm problem, because:
	- $Q=kP$, is equivalent to $Q=P^k$

**Elliptic Curve on Galois Field**
- Uses integer points only
- Has the form $y^2=x^3+ax+b\text{ (mod p)}$
- All operations are done using $\text{mod }p$.

## Elliptic Curve in Cryptography
- Expansion of public key:
	- Elliptic Curve Elgamal (ECEG)
	- Elliptic Curve Digital Signature (ECDSA)
	- Elliptic Curve Diffie-Hellman (ECDH)
- Any cryptographic algorithm/protocol that uses DLP can be adapted to using Elliptic Curve
- Properties:
	- Elliptic Curve Equation:
		- $a, b$
		- prime $p$
	- Elliptic Group
		- calculated using equation
	- Base Point $B \text{ or } G$.
- Keys:
	- Private: $x$, chosen from $[1, p-1]$
	- Public: $Q$. $Q=x\cdot B$