# Symbols
## General

| Symbol        | Meaning          |
| ------------- | ---------------- |
| $\therefore$  | Therefore        |
| $\in ,\notin$ | In (set)         |
| $\mid$        | Such that        |
| $\mathbb{R}$  | Real numbers     |
| $\mathbb{Q}$  | Rational numbers |
| $\mathbb{Z}$  | Integers         |
| $\mathbb{N}$  | Natural numbers  |
## Logic

| Symbol            | Meaning        |
| ----------------- | -------------- |
| $\to$             | Implies        |
| $\implies$        | Implies        |
| $\therefore$      | Therefore      |
| $\because$        | Because        |
| $\leftrightarrow$ | Iff            |
| $\iff$            | If and only if |

# Laws
**Contrapositve Law**
$$P\to Q \text{ is equivalent to }\neg Q\to \neg P$$
Useful to prove something when the contrapositive is easier to prove.

**Exercise 11.b Section 1.5**
$$(P\lor Q)\leftrightarrow Q \text{ is equivalent to } P\to Q$$
$$(P\land Q)\leftrightarrow Q \text{ is equivalent to } Q\to P$$

**Quantifier Negation Law**
$$\neg \exists xP(x)\text{ is equivalent to }\forall x \neg P(x)$$
$$\neg \forall xP(x)\text{ is equivalent to }\exists x \neg P(x)$$
Combining these with De Morgan and other equivalence laws, we can often reexpress *negative statements* as an equivalent but easier to understand *positive statement*

# Tips

>[!note] Examples
>All the examples given in the book are very important

>[!important] Choosing Definitions
>When working out the meaning of complex mathematical statement, it is important to choose which definition to think about first. **Always start with the "outermost" symbol.** 

>[!warning] Importance of Logical Symbols
>Writing complex math symbols/notation in terms of logical symbols can make the statement easier to understand.

# Proof Strategies
> [!info] Strategy 1
> To prove a conclusion of the form $P\to Q$:
> First assume that $P$ is true, then prove $Q$.
> Or alternatively:
> First assume that $Q$ is false, then prove that $P$ is false (*contrapositive equivalence*).

> [!info] Strategy 2
> To prove a goal of the form $\neg P$
> If possible, transform into some other form, then proof this other equivalent form

> [!info] Strategy 3
> To prove a goal of the form $\neg P$
> Assume $P$ is true, then try to reach a contradiction. Once a contradiction is reached, we will know that $P$ is false.
> In other words, try to prove $P$.

## Summary of Proof Ways
- *Proof by Contradiction*