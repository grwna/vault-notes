> [!warning] Foreword
> The materials in this section is heavily *practice based*. The contents written will generally be brief, and serve only to show the overview of how a strategy or technique works. 
>
> To truly understand the strategy or technique, practice using examples or exercises from the book.
# Conjunctive Statements
This is very simple.

>[!info] Strategy 10
>**To prove a goal of the form $P\land Q$**
>Prove $P$ and $Q$ separately. That is, they are treated as two different goals.
>
>**To use a given of the form $P\land Q$**
>Treat is as two separate givens, $P$ and $Q$.

#  Biconditional Statements
The strategies for conjunctive statements lend us the ability to deal with statements of the form ($P\leftrightarrow Q$), that is, treat it as two different givens/goals. **However**, keep in mind that you have to separate the givens and goals list, as it can lead to a point where you assumed both sides of the statement true. In other words, treat both statements as different *questions*, instead of just different goals.

Being able to deal with these types of statements allow us to prove *equality*.

When writing the proof, each part is usually denoted with left or right arrow. 
Example:
*Proof*
($\rightarrow$) Suppose $x$ is even
($\leftarrow$) Suppose $x$ is odd

When using givens with biconditionals, split the given into two conditional. statements.

**String of Equivalences**
$$P \iff R \iff Q$$
Understand what this means, and see how it's used. (Page 150).
In short, this is the:

> *Technique of figuring out a sequence of equivalence in one order, then writing it in the reverse order*

Which is used often in proofs. You may use it without realizing it while manipulation equalities.

> [!tip]
> Page 137 mentions that *almost* every proof that two sets are equal involve one of these approaches:
> Let $A$ and $B$ be sets.
> To prove $A=B$ we can use one of these:
> - $x\in A\leftrightarrow  x\in B$
> - $A \subseteq B\land B\subseteq A$
>
>Either works.


# Disjunctive Statements
A given of the from $P\lor Q$ tells you that either $P$ or $Q$ is true, but it doesn't tell you which one is true. Therefore, in order to use it, you must consider all possibilities. This is called *proof by cases*.

>[!info] Strategy 11
>**To use a given of the form $P\lor Q$**
>Break the proof into cases:
>- For case 1, assume $P$ is true, then prove the goal
>- For case 2, assume $Q$ is true, then prove the goal
>
>Both cases must lead to the goal.

The cases must be *exhaustive*, but they need not be *exclusive*. 
>[!tip] 
>Keep in mind that disjunctive statements can **always** be converted into conditional statements. Knowing which of these forms to use for a certain form of a goal is very important.

*Proof by cases* can also be useful for goals of the form $P\lor Q$, especially if we also have givens of the form $P\lor Q$. Note that in this case, you only need to prove one of the statements ($P$, or $Q$).

>[!info] Strategy 12
>**To prove a goal of the form $P\lor Q$**
>Prove one of the statements.
>If you have a given with disjunctions, break the proof into cases , in each case prove one of the statements.

Sometimes it is still useful to break proof into cases even if there is no disjunctive givens. Remember that the *disjunctive givens* only **helps** in finding relevant cases, if no such givens are available, the cases are not immediately obvious but you can still figure out the cases. (See example 3.5.3) for more details.

If you find it difficult to break the cases, a good rule of thumb is to simply assume $P$ is true in one case, and $P$ is false in another case. This is *exhaustive* so it is enough. In case 1, prove $P$, in case 2, prove $Q$.

>[!info] Strategy 13
>**To prove a goal of the form $P\lor Q$**
>- If $P$ is true, clearly $P\lor Q$ is true
>- If $P$ is false, prove that $Q$ is true
>
>Notice that you only really need to worry about case 2, since case 1 is trivial.

Also notice, that this is basically the same process if you converted the form $P\lor Q$ into it's conditional equivalence, $\neg P\to Q$.

Another way to prove this form is to use *disjunctive syllogism*. You can think of this as *modus ponens*, but the statement is of the form $\neg P\to Q$.