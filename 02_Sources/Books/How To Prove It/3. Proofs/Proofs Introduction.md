Proof writing is like completing a jigsaw puzzle. It requires building a complete picture by using small building blocks. Sometimes you might connect some puzzle pieces incorrectly, so you have to take them apart, then test out other puzzle pieces for it.

# Theorems
Mathematicians usually state the answer to a question in the form of a *theorem*. It states that if some assumption (called the *hypotheses*) of a theorem are true, then some conclusion must also be true.

The hypotheses and conclusion uses free variables, which are elements within the universe of discourse. A particular value that is assignable to the free variable is called an *instance*. A theorem is true if for every instance within $U$ where the hypotheses is true, then the conclusion is also true. In other words:
Let 
- $u$ stand for a specific instance
- $H$ is for hypotheses
- $C$ is for conclusion
$$\forall u\in U(H(u) \to C(u))$$
Which means the theorem is incorrect if $\exists  u\in U(H(u) \land  \neg C(u))$. Such instance $u$ is called the *counterexample* of the problem.

**Example**
$$\text{Supppose } x>3 \text{ and } y<2 \text{. Then } x^2-2y>5$$
Here, the statements after *suppose* are the hypotheses, and the statements after *then* are the conclusion.

>[!note] Difficulty of Proofs
>For some problems, it is *very difficult* to prove true, but easily proven false using a *counterexample*.

# Proof-Writing Techniques
How we figure out and write up a proof of a theorem will depend mostly on the logical forms of the conclusion, and often on the hypotheses aswell.

## Techniques Based on The Hypotheses's Form
This uses ways to draw *inferences* from the hypotheses (directly, or through some other inferences). You will then use these inferences to justify a certain *assertions* that some other statement is true.
**Example**
Say we're trying to prove the statement:
$$\text{if }n \text{ is an even integer, then } n^2 \text{ is also an even integer}$$
**Steps in Solving**
1. *Assertion*: suppose $n$ is an even integer (directly from the hypotheses)
2. *Inference*: an even integer can be written in the form $2k$ where $k$ is any integer (number theory)
3. *Assertion*: $n=2k$ (use assertion from 1. and inference from 2. to get this)

You can then chain the new assertion to another assertion using a certain *inference*, and eventually you will have proven that the statement is true.

> [!important] Assertions must guarantee truth
> It is important that every assertions made must be justified through inferences that guarantees the assertions are correct. This is to avoid incorrectly proving a theorem.


## Techniques Based on The Conclusion's Form
Different from before, these techniques uses ways of transforming the problem into an equivalent, but easier to solve problems. These often involves making assumptions and then proving based on that assumption. 

It is important to differentiate assertions with assumptions. While assertions guarantees truth, assumptions only guarantees that *if* the assumption is true, then the statement is true.

> [!info] Strategy
> To prove a conclusion of the form $P\to Q$:
> First assume that $P$ is true, then prove $Q$.
> Or alternatively:
> First assume that $Q$ is false, then prove that $P$ is false (*contrapositive equivalence*).

Basically, this means that we move $P$, which is previously in the conclusion, into the list of hypotheses. This makes easier because instead of proving $P\to Q$, we only have to prove $Q$.

## Givens and Goals
Proving a certain conclusion may require building blocks, that is using assertions we made to prove a certain smaller conclusion that, in the end, will help with proving the main conclusion. These intermediary hypotheses and conclusions will be called *givens* and *goals*. While hypotheses and conclusions signify the main or starting point that we have to prove something, givens and goals are more general.

However, givens and goals are usually used only for the *scratch work*, and will not be used in the final write-up that people read. This can make proofs hard to read since the strategy of how the writers come up with them is abstracted away.

> [!summary] Tips
> The logical form of a statement makes proofs easier. This makes it important to know the definition of mathematical terms, so that you know how to get the logical forms of them.
>
>I missed this while taking notes, but understanding the final form of a proof makes it easier to construct a presentation of a proof (instead of just the *scratch work*).



