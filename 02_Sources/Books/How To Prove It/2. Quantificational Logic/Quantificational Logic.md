- [[#Keywords|Keywords]]
- [[#Quantifiers|Quantifiers]]
	- [[#Quantifiers#Introduction|Introduction]]
	- [[#Quantifiers#The Orders of Quantifiers Matter|The Orders of Quantifiers Matter]]
	- [[#Quantifiers#Translating English to Quantificational Logic|Translating English to Quantificational Logic]]
	- [[#Quantifiers#Translating Quantificational Logic to English|Translating Quantificational Logic to English]]
- [[#Equivalences Involving Quantifiers|Equivalences Involving Quantifiers]]
	- [[#Equivalences Involving Quantifiers#Quantifier Negation Laws|Quantifier Negation Laws]]
	- [[#Equivalences Involving Quantifiers#Uniqueness Quantifier|Uniqueness Quantifier]]
	- [[#Equivalences Involving Quantifiers#Bounded Quanfiers (Universe of Discourse)|Bounded Quanfiers (Universe of Discourse)]]
	- [[#Equivalences Involving Quantifiers#Quantifiers on Empty Sets|Quantifiers on Empty Sets]]
	- [[#Equivalences Involving Quantifiers#Validation of Quantificational Statements|Validation of Quantificational Statements]]
- [[#Closing Remarks|Closing Remarks]]
- [[#Exercises|Exercises]]

# Keywords
- Universal Quantifier
- Existential Quantifier
- Quantifier Negation Law
- Uniqueness Quantification
- Bounded Quantifiers

# Quantifiers
## Introduction
To say that $P(x)$ is true for every value of $x$ in $U$, we write $\forall xP(x)$. It reads "For all $x$, $P(x)$." or "For all $x$, $P(x)$ is true". This is equivalent to saying that the [[Variables and Sets#Truth Set|truth set]] of $P(x)$ is $U$.

We also write $\exists xP(x)$ to say that at least one value of $x$ makes $P(x)$ true. This is equivalent to saying the truth set of $P(x) \neq\varnothing$.

We can then write the example given in [[Conditional and Biconditional Connectives#Conditional Statement|conditional statements]] as:
$$\forall x(x>2\to x^2>4)$$
>[!important]
>Quantifiers *bind* a variable. This means the variables next to a quantifier symbol are always *bound variables*

"Words such as *everyone*, *someone*, *everything*, or *something* are often used to express the meanings of statements containing quantifiers."

The form of *quantifiers applied to a conditional statement* happens often and is very **important** to understand it.

We can use multiple quantifiers in a statement to better represent a statement. For example, the statement "*All parents are married*" can be represented as:
$$\forall x(\exists yP(x,y)\to \exists zM(x,z))$$
Where,
- $P(x,y)$ - $x$ is a parent of $y$
- $M(x,z)$ - $x$ is married to $z$
**Please note** that the usage of quantifiers in the statement is **very important**, so that the variables are bounded.

>[!note]
>How do we comprehend multiple quantifiers in a statement?
>$$\forall x \exists y(x+y=5)$$
>Think about the $\forall$ first, take it out and get the rest of the statement. Then understand the statement without the $\forall$.
>
>In this case, the statement above means "*no matter what value of x you choose, there will always be atleas one y for which x + y = 5 is true*"

## The Orders of Quantifiers Matter
In the note above, if we swapped the quantifiers:
$$\exists y\forall x (x+y=5)$$
This now means: "*There is a value for y in which no matter what x you choose, x+y=5*"
It should be clear that this statement is false.

>[!note]
>The order of quantifiers *does not matter* if the quantifier is the same.
>Example: 
>$$\exists y\exists x(x+y=2) \text{   is equivalent to   }\exists x \exists y(x+y=2)$$
>We can interpret these as meaning:
>- $\exists x\exists y$ - there are $x$ and $y$ such that
>- $\forall x\forall y$ - for all $x$ and $y$
>In which the order is *interchangeable*, and $x=y$ is a possibility. You must add $\dots \land x\neq y$.

## Translating English to Quantificational Logic
The rule of thumb is:
- $\forall$ will use $\to$
	**Example:** "*All humans are mortal*"
	Then the most natural interpretation is: "*If it is human, then it is mortal*"
- $\exists$ will use $\land, \lor$
	**Example:** "*Some humans are mortal*"
	Interpretation: "*There exists something that is a human AND it is mortal*"
This generally holds for their negations as well.

## Translating Quantificational Logic to English
If there are two quantified variables, if they *interact* ($x$ likes $y$, $x$ is related to $y$), then use two quantifiers outside the parentheses.

# Equivalences Involving Quantifiers

Using equivalences, we can reexpress unintuitive statements into ones we can easily comprehend. 

## Quantifier Negation Laws
$$\neg \exists xP(x)\text{ is equivalent to }\forall x \neg P(x)$$
$$\neg \forall xP(x)\text{ is equivalent to }\exists x \neg P(x)$$
Combining these with De Morgan and other equivalence laws, we can often reexpress *negative statements* as an equivalent but easier to understand *positive statement*

>[!warning]
>Be careful how you apply the negation.
>Also, remember that when two statements are equivalent, then the negation of both statements are also equivalent.

Example of quantifier negation law application:
"*Everyone who Patricia likes, Sue doesn't like*"
$$\forall x(L(p,x)\to \neg L(s,x))$$
$$\forall x(\neg L(p,x)\lor \neg L(s,x)) \tag{conditional law}$$
$$\forall x\neg(L(p,x)\land L(s,x)) \tag{De Morgan's law}$$
$$\neg\exists x(L(p,x)\land L(s,x)) \tag{quantifier negation law}$$
The final statement that we got means "*There's no one that both Patricia and Sue likes*". And this might be easier to understand than the first statement.

## Uniqueness Quantifier
In [[#Exercises|exercise 1]], we encounter a statement that uses **exactly one** of something. This occurs often in mathematics that there is a special notation for it (called the *Uniqueness Quantifier*):
$$\exists!xP(x)$$
This is equivalent to the form: $$\exists xP(x)\land \neg \exists y(P(y)\land y\neq x)$$
## Bounded Quanfiers (Universe of Discourse)
To write specific constraints for the *universe of discourse*, we can add a specifier. 
Example:
$$\forall x \in \mathbb{R}(x\geq0) \text{ or }\forall x \in \mathbb{N}(x\geq0)$$
We can also use other notations, such as (not limited to):
$$\forall x>0(x\geq0)$$
These *bounded quantifiers* are like abbreviations of more complex statements, since you can write these *bounds* (i.e. $\forall x(x\in A\land P(x))$). This means that laws like *quantifier negation law* works for bounded quantifiers.

## Quantifiers on Empty Sets
Say that $A =\varnothing$ , these statements are (no matter what $P(x)$ is):
- $\exists x\in A(P(x))$ - always false [stmt 1]
- $\forall x\in A(P(x))$ - always true [stmt 2]
The first one should be clear. But how come the second one is *always true*?
There are two ways to verify this:
**Convert to Conditional Form**
$\forall x\in A(P(x))$ can be written as:
$$\forall x(x\in A\to P(x))$$
Now since the *[[Conditional and Biconditional Connectives#Conditional Statement|antecedent]]* is always false, this means the *conditional statement* is always true (why? read conditional logic again).

**Negation**
$\forall x\in A(P(x))$ is equivalent to:
$$\neg \neg \forall x\in A(P(x))=\neg (\neg \forall x\in A[P(x)])\tag{double negation law}$$
$$\neg (\exists xA[\neg P(x)])\tag{quantifier negation law}$$
$$\neg\exists xA(\neg P(x))$$
If you look closely, that is the negation of the first empty set statement, which is always false. Negation of always false is always true (*vacuously true*).

How can this fact be applied? one such application is the **proof** that empty sets are a subset of any set. Why?, first we see from the quantified notation of a subset:
We say $A\subseteq B$ is equivalent to $\forall x(x\in A\to x\in B)$, which is equivalent to:
$$\forall x\in A(x\in B)$$
And we can see that this is similar to the form of [stmt 2], which is *vacuously true* if $A$ is the empty set.


## Validation of Quantificational Statements
Previously, we were able to validate equivalences on *logical statements* by using **truth tables**. This cannot be done with statements involving *quantifiers*. Currently our method is to look at examples and use common sense. In chapter 3 we will develop **better methods** for this.

Here are some laws that apply to quantifier logic:
- Universal quantifier *distributes over conjunction*
- Existential quantifier *distribute over disjunction* (you can prove this using the above statement)
What does that mean? it means $\forall x(P(x)\land Q(x))$ is equivalent to $\forall xP(x)\land \forall x(Q(x))$.
An application of this, is the proof that $A=B$ is equivalent to $A\subseteq B\land B\subseteq A$ (read page 75 [88 pdf]).

# Closing Remarks
We have now come to a close for the logical theory part of the book. The seven symbols we have learned ($\land,\lor, \neg, \to, \leftrightarrow, \forall, \exists$) are powerful and **the structure of all mathematical statements** can be understood using these symbols. To illustrate the power of these symbols, read Example 2.2.3 (page 75 [89 pdf])
# Exercises
1. Analyze the logical forms of the following statements.
	- John likes exactly one person
The answer to that is: $$\exists x(L(j,x)\land \neg \exists y(L(j,y)\land y\neq x))$$Where: 
- $L(x,y)$ - $x$ likes $y$
- $j$ - John
