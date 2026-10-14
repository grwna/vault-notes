- [[#Keywords|Keywords]]
- [[#Variables|Variables]]
- [[#Sets|Sets]]
	- [[#Sets#Set Definition|Set Definition]]
	- [[#Sets#Free and Bound Variables|Free and Bound Variables]]
	- [[#Sets#Truth Set|Truth Set]]
	- [[#Sets#Subsets and Supersets|Subsets and Supersets]]
- [[#Operations on Sets|Operations on Sets]]

# Keywords
- Free/Bound Variables
- Truth set
- Universe of Discourse
- Empt Set
- Venn diagram
- Symmetric Difference

# Variables
Some examples of variable usage are:
- $P(x)$ - $x$ is a prime number
- $D(p,q)$ - $p$ is divisible by $q$
- $M(x)$ - $x$ is a man

**Variable Truth Values**
In, [[Deductive Reasoning and Logical Connectives#Truth Tables|Truth Tables]], we assign truth values directly to statements. We can't do this with variables, because variables can have different values. For example: $P(x)$ would be true if $x=23$ but not if $x=22$.

To deal with this, we can use *truth sets* for statement containing variables.

# Sets
A set is a collection of objects. 
- Orders does not matter. 
- Duplicates does not matter.
A set is completely determined once its elements have been specified. Thus, two sets that have the same elements are always equal.

## Set Definition
So we don't have to write out all the elements of a set, we can use mathematical notations.
For example, a set containing prime numbers can be notated as:
$$B=\{x\mid x \text{ is a prime number}\}$$
B is equal to the set of all x such that x is prime number.

The statements after $\mid$ is the *elementhood test*, or the filter function for elements of the set. 

## Free and Bound Variables
$$y\in\{x \mid x^2<9\}$$
y is the free variable and x is the bound variable.
The free variable stands for objects that the statement is about. Plugging in different values for a free variable affects the meaning of a statement and may change its truth value.
A bound variable doesnt stand for anything, and it can be replaced. Think of it as an intermediate variable (locally scoped in a program's block)

>[!note]
>Several important note:
>- $y\in\{x \mid x^2<9\}$ is equal to $P(y)$
>- $y\notin\{x \mid x^2<9\}$ is equal to $\neg P(y)$
>- $y\in\{x\mid x \text{ is divisible by }w\}$ - y and w are both free variables
>- $2\in\{w\mid 6\notin\{x\mid x\text{ is divisible by }w\}\}$
>In the last point, there are no free variables, and therefore the statement's truth value does not depend on any variable and we can assign it directly

The expression $\{x\mid P(x)\}$ is not a statement, but rather a name for a set.
**It is very important** to distinguish between expressions that are mathematical statements and expressions that are  names for mathematical objects.

## Truth Set
The truth set of a statement, for example the statement $P(x)$, is the set of all values of $x$ that makes the statement $P(x)$ true. Or in other words:
$$\text{truth set}=\{x\mid P(x)\}$$
>[!important]
>This definition applies for statements with 1 *free variables*. Multiple free variables's truth set will be explored in Chapter 4.

**Universe of Discourse** (denoted as $U$) for a statement is all possible values of a free variable in the statement.
Common *universe of discourse* in math are: $[\mathbb{R},\mathbb{Q},\mathbb{Z},\mathbb{N}]$. 
Example usage in set notation:
$$y\in \{x\in\mathbb{R}\mid x^2<9\}$$
Which means the same thing as:
$$y\in \mathbb{R}\land y^2<9$$
>[!note]
>$\mathbb{R}^+$ means positive real numbers only
>$\mathbb{Z}^-$ means negative integers only

A truth set of a statement can contain the entire universe $U$, or nothing (empty set $\varnothing$). This is similar to the concept of [[Deductive Reasoning and Logical Connectives#Tautologies and Contradictions|Tautologies and Contradictions]].

>[!note]
>$\varnothing$ is an empty set $\{\varnothing \}$ is a set containing an empty set

## Subsets and Supersets
**Subsets**
We say $A\subseteq B$, ($A$ is a *subset* of $B$), if every element of $A$ is also an element of $B$.

**Disjoints**
Two sets $A$, and $B$ are *disjoint* if $A\cap B=\varnothing$

**Example of Mathematical Proofs using Deductive Reasoning**
![[Pasted image 20251129163923.png|500]]


# Operations on Sets
Basic set operations
**Intersection**
$$A\cap B=\{ x\mid x \in A \text{ and } x\in B \}$$
**Union**
$$A\cup B=\{ x\mid x \in A \text{ or } x\in B \}$$

**Difference**
$$A\setminus B=\{ x\mid x \in A \text{ and } x\notin B \}$$

**Venn Diagrams** makes it easier for us to understand operations on sets.

**Symmetric Difference** (the XOR of set operations)
$$A\triangle B = (A\setminus B)\cup(B\setminus A)=(A\cup B)\setminus(B\cup A)$$
This is the opposite of intersection.

**Connections of Set Operations and Logical Connectives**
If $A$ is the truth set of $P(x)$ and $B$ is the truth set of $Q(x),$ what is the truth set of $P(x)\land Q(x)$, $P(x)\lor Q(x)$, and $\neg P$?

We can use set operations to define them:

| Logical          | Set            |
| ---------------- | -------------- |
| $P(x)\land Q(x)$ | $A\cap B$      |
| $P(x)\lor Q(x)$  | $A\cup B$      |
| $\neg P$         | $U\setminus A$ |
Keep in mind however, that they are not interchangeable, as their operands are different.
Laws of equivalence (read: [[Deductive Reasoning and Logical Connectives#Equivalences|Equivalences]]) for logical connectives also works with sets.

>[!note]
>The distributive laws require **two different** operators. If it has the same operators, then it uses commutative laws in tandem with idempotent laws instead.



