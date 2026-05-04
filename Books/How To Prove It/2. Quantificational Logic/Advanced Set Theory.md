# Keywords
- Index Family
- Index Set
- Families of Sets
- Power Set

# Advanced Set Notation
Now that we are familiar with *[[Quantificational Logic#Quantifiers|quantifiers]]*, we can discuss more advanced topics in set theory. For example, we previously defined a set this way, lets say $S$ is the set of all perfect squares:
$$S={\{ x^2\vert x\in \mathbb{N}\}}$$
We can now define the same set this way:
$$S=\{ x \; \vert \;\exists n\in\mathbb{N}\,(n^2=x) \}$$
# Indexed Family
Let's say we want to define a set for the first 100 prime numbers. We can define the $i$-th prime number as $p_{i}$ , then the set would be $P=\{ p_{1}, p_{2}, \dots,p_{100} \}$. Another way to say this is to define $P$ as: 
$$P={\{ p_{i} \;\vert\; i\in I\}}$$
Where:
$$I=\{ i\in\mathbb{N}\;\vert\; 1\leq i\leq 100 \}$$
Here, $P$ is called the *indexed family* and $I$ is called the *index set*. The *index* does not have to be numbers. You can think of the index as a "key" like in a hash map.
>[!note]
>In general, any *indexed family*:
>$$A=\{ x_{i} \;\vert\; i\in I \} \;\text{ can also be defined as } \; A=\{ x \;\vert\; \exists i\in I(x=x_{i}) \}$$
>And consequently:
>$$x\in \{ x_{i} \;\vert\; i\in I\} \equiv \exists i\in I(x=x_{i})$$

# Families of Sets
Sets containing sets. Lets say $A=\{ 1,2,3 \}$, and $\mathcal{F}={\{  A\}}$, here $1\in A$ but $1\notin \mathcal{F}$.

## **Families of Sets as Indexed Family**
Lets say $S$ is the set of all students. And for each student, $C_s$ is the set of courses that they take. Then we can define the family of sets as: 
$$\mathcal{F}=\{ C_{s} \;\vert\;s\in S \}$$
Note that each $C_{s}\in\mathcal{F}$ but a specific course $c\in C_{S}$ is not in $\mathcal{F}$.

## **Union and Intersection of Family of Set**
Denoted by $\bigcup \mathcal{F}$ and $\bigcap \mathcal{F}$. Are operations that does Union or Intersection on all sets within a family set. These notations are called the **big unions/intersections**
In the example before:
- The union is the set of all courses that has been taken by *any students*
- The intersection is the set of courses that is taken bby *all students*

The formal definition of these sets are the following:
- $\bigcap \mathcal{F}=\{ x \;\vert\; \forall A\in \mathcal{F}(x\in A) \}$
- $\bigcup \mathcal{F}=\{ x \;\vert\; \exists A\in \mathcal{F}(x\in A) \}$

In the book, these sets are undefined if $\mathcal{F}=\varnothing$

> [!Note] More on Empty Sets
> It is interesting to note [[Quantificational Logic#Quantifiers on Empty Sets|Quantifiers on Empty Sets]] on the behaviour of the **big operators**.
> Note the false and the vacuously true statement. What is interesting is that most mathematicians consider the notation $\bigcap \varnothing$ to be useless due to this fact.

## **Indexed Union and Intersection of Family Sets**
To denote unions and intersections of family sets for a specific indexed groups of sets, there is a special notation
$$\bigcap \mathcal{F}=\bigcap\limits_{i \in I}A_{i}=\{ x\;\vert\; \forall i \in I (x\in A_{i})\}$$
$$\bigcup \mathcal{F}=\bigcup\limits_{i \in I}A_{i}=\{ x\;\vert\; \exists  i \in I (x\in A_{i})\}$$
>[!important]
>Study how the distribution laws work for both unions and intersections. 
>Also study how unions and intersections affect the equivalences of sets.

## **Universe of Discourse for Families of Sets**
When discussing the sets whose elements are sets, it might seem natural to consider the universe of discourse to be the set of all sets, but this leads to a contradiction.

Suppose that $U$ is the set of all sets, since $U$ itself is a set, then it *should* be true that $U \in U$. This suggests that the sets in $U$ can be split into two:
- The unusual sets, where it is an element of itself
- Regular sets that are not elements of themselves
If we let $R$ be the regular sets, that is $R=\{ A\in U\;\vert\; A \notin A\}$. In other words:
$$\forall A \in U (A\in R \iff A \notin A)$$
Now, since $U$ is the set of all sets, then $U$ must contain $R$, which allows us to substitute $A$ with $R$, which makes the statement:
$$\forall R \in U (R\in R \iff R \notin R)$$
Here we can see that the conditional statement ($\iff$)  is a paradox, this is called the **Russel's Paradox**.

This implies several things regarding sets:
- Not every collection is a set
- Sets must be built, not just defined:
	- **The Axiom of Specification**: you can only form a new set by picking elements from an already existin set that satisfy a property.
- **Structural Regularity**: the membership relation ($\in$) cannot be circular.
# Power Set
A power set of a set $A$, denoted $\mathcal{P}(A)$ is the *family of sets* that contains all subsets of $A$. 

>[!example]
>Say $A=\{1,5\}$, then $\mathcal{P}(A) = \{ \varnothing, \{ 1 \}, \{ 5 \}, \{ 1,5 \} \}$
>Also, $\mathcal{P}(\varnothing)=\{ \varnothing \}$.
>
>Do note that: $\{ \varnothing \}=\varnothing$

Notice that the $A$ appears inside the powerset. This gives the characteristics:
$$A\in \mathcal{P}(A)$$
Also, **to say that $x\in \mathcal{P}(A)$ is equivalent to saying that $x\subseteq A$**, which means:
$$x\in \mathcal{P}(A) \iff \forall y(y\in x\to y\in A)$$
Basically, all members of a powerset of a set $A$ are the subsets of $A$:
$$\forall x (x\in \mathcal{P}(A)\to x\subseteq A)$$

**Some Characteristics of the Power Set**
- As in before, $x\in \mathcal{P}(A)$ is equivalent to $x \subseteq A$
- $x\in \mathcal{P}(A\cap B)$ is equivalent to $x\in \mathcal{P}(A)\cap \mathcal{P}(B)$. This *does not apply* for $\cup$

# **Equivalent Notations (Example 2.3.1)**
How do we write the logical form of: $\{ x_{i} \;\vert\; i\in I\}\subseteq A$
One way to write it is to decompose each statement. 
1. First we decompose the subset:
	$$\forall x(x\in \{ x_{i} \;\vert\; i\in I\} \to x\in A)$$
2. Then we decompose the set membership of x statement:
$$\forall x(\exists i\in I(x=x_{i})\to x\in A$$

And thus we found the logical form of the statement. However a different way to say it exists. The original statement is equal to saying "*All elements of $x_{i}$ such that $i$ is in the Index Set is also an element of $A$*".
Thus another way to write the original statement is:
$$\forall i\in I(x_{i}\in A)$$
But how do we show that this is **truly** equivalent to the orignal statement? we will learn a way to show this in *Chapter 3: Proofs*.



