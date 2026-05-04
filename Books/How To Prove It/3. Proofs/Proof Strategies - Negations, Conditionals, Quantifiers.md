warning] Foreword
> The materials in this section is heavily *practice based*. The contents written will generally be brief, and serve only to show the overview of how a strategy or technique works. 
>
> To truly understand the strategy or technique, practice using examples or exercises from the book.
# Negative Statements
It is easier to prove a positive statement (what *should* be true) instead of proving a negative statement (what *shouldn't* be true). Therefore, it is beneficial to transform the logical form into a positive statement.

> [!info] Strategy 1
> **To prove a goal of the form $\neg P$**
> If possible, transform into some other form, then proof this other equivalent form

If it is not possible to transform into a positive statement, it is usually best to do a *proof by contradition*.

> [!info] Strategy 2
> **To prove a goal of the form $\neg P$**
> Assume $P$ is true, then try to reach a contradiction. Once a contradiction is reached, we will know that $P$ is false.
> In other words, given $\neg P$, try to prove $P$.

When accounting for the goal's contradiction, add the contradiction into the given list.

For *proof by contradiction*, you can use *givens* in the form $\neg P$. For any other kinds of proofs, it is easier to reexpress $\neg P$ to some other forms.

> [!info] Strategy 3
> **To use given of the form $\neg P$**
> If possible, reexpress into some other form.

# Conditional Statements

> [!info] Strategy 4
> **To prove a goal of the form $P\to Q$**
> Suppose $P$ is true, then prove $Q$

So far, we have talked about goals of the form $P\to Q$, but what about given of that form?

> [!info] Strategy 5
> **To use given of the form $P\to Q$**
> If given $P$, or if you can proof $P$ is true, then you can conclude that $Q$ is true (*modus ponens*).
> If you can proof $Q$ is false, then you can conclude that $P$ is false, through *contrapositive law* (*modus tollens*).
> Otherwise, this given is not of much use.

 An example on how to apply the strategy above is *Example 3.2.4* at page 109.
 You can approach this by treating the *antecedent* of the conditional statements as the goal.
 Example:
 Given $x \in B\to x\in C$, prove $x\in C$.
 Instead of making $x\in C$ the goal, you can instead make  $x\in B$ the goal.


# Quantified Statements
In order to proof a goal of the form $\forall x P(x)$, we need to prove a goal $P(x)$ that would work no matter what $x$ was. For this, it is important that we do not make any assumptions about $x$. In other words, $x$ must be *arbitrary*, and cannot stand for some particular object already discussed and used within the proof (as a given).

>[!info] Strategy 6
> **To prove a goal of the form $\forall xP(x)$**
> Let $x$ stand for an arbitrary object, then prove $P(x)$.
> $x$ must be a *new* and *unused* variable.
> This means $x$ must not have been in the given list, but it can be added into the given list afterwards.


**Before using strategy:**

| Givens | Goals           |
| ------ | --------------- |
| -      | $\forall xP(x)$ |

**After using strategy:**

| Givens | Goals  |
| ------ | ------ |
| -      | $P(x)$ |
The rest of the proof should be similar to proofs with other forms of conclusion.

> [!hint] Recall
> The statement: $\forall x\in A P(x)$
> Is equivalent to: $\forall x(x\in A \to  P(x)$

Just like the form $\forall xP(x)$, proving a goal of the form $\exists xP(x)$ involves introducing a new variable. This variable however, does not have to be *arbitrary*. It suffices to assign any particular value to $x$ and prove $P(x)$ for this value.

>[!info] Strategy 7
>**To prove the goal of the form $\exists xP(x)$**
>Try to find a value for $x$ for which $P(x)$ will be true. 
>Then start the proof with "Let $x$ = (...)", and proceed to prove $P(x)$.
>Once again $x$ should be a *new* variable.

Finding the right value for $x$ may be difficult. One method is to assume $P(x)$ is true, then try to figure out what $x$ must be, based on the assumption. However, if this doesn't work, then any other method will do, including (but not limited to) guessing, trial-and-error, and using the given list to look for ideas.

Remember that in order to justify a conclusion of a proof, you only need to provide a valid reasoning. You do not need to show how you thought of such reasoning.

>[!info] Strategy 8
>**To use a given of the form $\exists xP(x)$**
>Introduce a *new* variable $x_{0}$ into the proof to stand for an object for which $P(x_{0})$ is true. Now you can assume that $P(x_{0})$ is true.
>This is called *existential instantiation*.

Using $\exists xP(x)$ is very different than proving $\exists xP(x)$, because when using it, you don't get to choose a particular value to plug in for $x$. You can assume that $x$ makes $P(x)$ true, but you cannot assume anything else about it.
**Example**
$\to$ There exists and even number $x$.
You can operate $x$ using any properties of an even number (you can treat $x$ as an even number), but you cannot choose any value for it, so we can't say whether $x=4$, $x=200$ or $x=1.000.000$.

On the other hand, you can choose the value of $x$ for a given of the form $\forall xP(x)$.

>[!info] Strategy 9
>**To use a given of the form $\forall  xP(x)$**
>You can plug in any value for $x$ that satisfies a certain condition (e.g. $x\in \mathbb{R}$), then conclude that $P(x)$ is true.
>This is called *universal instantiation*.

**Note**: for the quantifier's strategies, use **Example 3.3.4 & 3.3.5**, it helps a lot.

**Guideline**
- If you know something exists, give it a name $\to$ apply *existential instantiation* immediately
- If you know every value satisfies a condition, wait until it becomes useful $\to$ *universal instantiation* might only be useful when you know something more about the given (ex. $\forall x(P(x)\to Q(x))$, instantiation (let $x$ = $a$) is only useful when you know either $P(a)$ or $\neg Q(a)$
- When analyzing the logical form of a statement, no need to complete it until it's the most simple form. Only do what is necessary to the point that it can become useful. Simplify it further later when/if we need to.
- Pay close attention to whether a variable stands for a number, a set, or a collection of sets.
- At any given time, if solving a given would directly lead to solving the goal, you may make the solving of that given as your goal (page 125).

**As a last note:**
Theorem 3.3.7 at page 140 is an example of using proofs for number theory, read it well.

