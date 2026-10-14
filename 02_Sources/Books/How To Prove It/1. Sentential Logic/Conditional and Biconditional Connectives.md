- [[#Keywords|Keywords]]
- [[#Conditional Statement|Conditional Statement]]
	- [[#Conditional Statement#Biconditional Statement|Biconditional Statement]]
- [[#Truth Tables for Conditional Statements|Truth Tables for Conditional Statements]]

# Keywords
- Antecedent
- Consequent
- Converse
- Contrapositive

# Conditional Statement
$$
\begin{array}{l}
  P \to Q \\
  P \\
  \hline
  \therefore Q
\end{array}
$$
Using the logical connective $\to$.
The statement $P\to Q$ is equivalent to $\neg P\lor Q$ and also equivalent to $\neg (P\land \neg Q)$, and these statements can be connected using the logical connectives. In that statement, $P$ is the *antecedent* and $Q$ is the *consequent*.

An example of a valid conditional statement is 
$$\text{if } x>2\text{ then }x^2>4$$

| Notation           | Name           | Characteristic |
| ------------------ | -------------- | -------------- |
| $P\to Q$           | Normal         | Baseline       |
| $Q\to P$           | Converse       | Not Equivalent |
| $\neg Q\to \neg P$ | Contrapositive | Equivalent     |

>[!note]
>The contrapositive law is **very important** for mathematical proofs reasoning.
>An example of its usage:
>**Conjecture**: If $n^2$ is even, then $n$ is even.
>**Proof**: We can prove by using the contrapositive, If $n$ is *not* even, then $n^2$ is *not* even
>Let $n=2k+1$.
>$$n^2=(2k+1)^2=4k^2+4k+1=2(2k^2+2k)+1$$

Other ways to express $P\to Q$
- $P \text{ implies }Q$
- $Q\text{, if }P$
- $P \text{ only if }Q$
- $P \text{ is a sufficient condition for }Q$
-  $Q \text{ is a necessary condition for }P$


## Biconditional Statement
We say $P\leftrightarrow Q$ (read $P$ if and only if $Q$) to represent a conditional statement and its converse at once. That is:
$$P\leftrightarrow Q \equiv (P\to Q)\land(Q\to P)$$
Which is then equivalent to:
$$(P\to Q)\land (\neg P\to \neg Q)$$
This means the statement is true if the truth values of $P$ and $Q$ are equal.

>[!important]
>The difference between $if$ and $iff$ is very important in mathematics. And mistaking one for another is **never acceptable**.

# Truth Tables for Conditional Statements
Say we have the argument:
$$
\begin{array}{l}
  L \leftrightarrow (P\land C) \\
  \neg C \\
  \hline
  \therefore L\leftrightarrow P
\end{array}
$$
We can make the truth table, lets say we get:

| $L \leftrightarrow (P\land C)$ | $\neg C$ | $L\leftrightarrow P$ |
| ------------------------------ | -------- | -------------------- |
| T                              |          |                      |
Then to determine whether the argument is valid or not, we find a line such that *every premise* is true. Then from the truth value of the *conclusion* we can say:
- Conclusion is false - then the argument is invalid
- Conclusion is true- then the argument is valid