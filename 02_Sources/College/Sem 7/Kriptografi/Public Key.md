# Theory
**Basis**
- Factorization Problem
- Discrete Logarithm Problem (DLP)
- Elliptic Curve DLP
- Knapsack
- Doiphantine Equation

**Utilization**
- Ciphering
- Digital signatures
- Key exchange


# Algorithms
## RSA
**Properties**
- p, q
- n
- totient(n) = (p-1)(q-1)
- e, where GCD(e, totient) = 1
- d $\equiv e^{-1}\text{mod}(\text{totient(n)})$

**Ciphering**
- c = $m^e\text{mod }n$
- p = $c^d\text{mod }n$

**Weakness**
- Slow
- Heavy
- Man-In-The-Middle

## ElGamal
**Basis**
- Uses DLP
	- $g^x\equiv y \text{ mod }p$
	- p prime
	- g, y any integer
	- Find x
- Primitive Root
	- An integer $a$ is a primitive root of $n$ if $a^{i}\equiv \text{mod }n$ produces a unique number for each $i$, where $i\in[0,\phi(n)]$
- If $a$ is a primitive root of a prime $p$, then for $b$ we can find $x$ for:
	- $b\equiv a^x \text{mod }p$

**Properties**
- $p$
- random $g$ ($g<p$, $g$ is primitive root of $p$)
- random $x$ ($2\leq x\leq p-2$)
- $y=g^x \text{mod }p$
- $m$ = plaintext
- $a, b$ = ciphertexts
- Public keys: triple$(y, g, p)$
- Private keys: tuple$(x, p)$

**Encryption**
- Pick random $k$ with the same rule as picking $x$ 
- $a=g^k \text{mod }p$
- $b=y^km \text{ mod }p$
- Ciphertext is twice the size of plaintext

**Decryption**
- Calculate $(a^x)^{-1} = a^{p-1-x} \text{mod }p$
- Plaintext $m=b(a^x)^{-1}\text{mod }p$
- The $k$ will be cancelled out automatically

## Diffie-Hellman Key Exchange
Besides Diffie-Hellman, you can use Hybrid cryptography: Encrypt message with AES, encrypt key with RSA.
**Properties**
- Two parties each have one pair of keys, public and private. (A,a, B, b)
- Prime $p$ (modulus), generator $g$, both public

**Protocol**
- Calculate public keys: 
	- $A=g^a \text{mod }p$
	- $B=g^b \text{mod }p$
- Derive shared secret 
	- $K=A^b \text{mod }p$
	- $K=B^a \text{mod }p$
	- It can be seen that $K$ from both results in the same valur

**Weakness**
- Man-in-the-middle

## Knapsack Merkle-Hellman
Normal knapsack only allows encryption, without decryption (decryption is NP-hard). For encryption and decryption you need to use **Superincreasing Knapsack**.

However **SE** is easy to break in linear time. However, you can modify **SE** to non-SE using public and private keys.

**Procedure**
- Pick a superincreasing sequence
- Multiply each element in sequence with $n \text{ mod }m$
	- $m$ larger than the sum of all elements
	- $n$ relatively prime to $m$
- Then the keys are:
	- Public: the multiplied sequence
	- Private: the original sequence

**Encryption**
- Use Public key
- Break plaintext's bits into groups with the length of sequence
- Multiply each bit by the corresponding sequence elements (by indices). This results in the ciphertexts.

**Decryption**
- Calculate $n^{-1} \text{mod }m$
- Multiply the ciphertexts with $n^{-1}$. This results in the total sum of knapsack, which you can use to solve the knapsack problem (finding bit 1 or 0) in linear time.