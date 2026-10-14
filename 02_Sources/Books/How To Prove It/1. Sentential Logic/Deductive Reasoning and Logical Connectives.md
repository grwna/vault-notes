
- [[#Keywords|Keywords]]
- [[#Deductive Reasoning|Deductive Reasoning]]
- [[#Truth Tables|Truth Tables]]
- [[#Laws of Logic|Laws of Logic]]
	- [[#Laws of Logic#Equivalences|Equivalences]]
	- [[#Laws of Logic#Tautologies and Contradictions|Tautologies and Contradictions]]

# Keywords
- Well-formed formulas
- Truth tables
- Equivalent formulas
- Tautology
- Contradiction

# Deductive Reasoning
Deductive reasoning is the foundation of which proofs are based.

An argument is *valid* if the premises cannot all be true without the conclusion being true as well. In short, if **all** the premises are true, then the conclusion **have** to be true.

Grammatically correct statements in logic are called *well-formed formulas.*
$\neg$ - negation
$\land$ - conjunction 
$\lor$ - disjunction

# Truth Tables
**How to make compact truth tables**
![[Pasted image 20251124192415.png|450]]
Instead of having separate columns for all intermediate statements, write the columns **under** the symbols. For more details, read How to Prove It Page 17 (31 PDF).

# Laws of Logic
## Equivalences
**De Morgan’s laws** 
- ¬(P ∧ Q) is equivalent to ¬P ∨ ¬Q. 
- ¬(P ∨ Q) is equivalent to ¬P ∧ ¬Q. 
**Commutative laws** 
- P ∧ Q is equivalent to Q ∧ P. 
- P ∨ Q is equivalent to Q ∨ P. 
**Associative laws** 
- P ∧ (Q ∧ R) is equivalent to (P ∧ Q) ∧ R. 
- P ∨ (Q ∨ R) is equivalent to (P ∨ Q) ∨ R. 
**Idempotent laws** 
- P ∧ P is equivalent to P. 
- P ∨ P is equivalent to P. 
**Distributive laws** 
- P ∧ (Q ∨ R) is equivalent to (P ∧ Q) ∨ (P ∧ R). 
- P ∨ (Q ∧ R) is equivalent to (P ∨ Q) ∧ (P ∨ R). 
**Absorption laws** 
- P ∨ (P ∧ Q) is equivalent to P. 
- P ∧ (P ∨ Q) is equivalent to P. 
**Double Negation law** 
- ¬¬P is equivalent to P.

Most of these will be intuitive as follows with algebra laws.
The only one that would be difficult to remember is *absorption laws*. 
A good way to think about it is that the P **absorps** (because its stronger) than what is inside the parentheses. 

## Tautologies and Contradictions
**Tautologies** - Formulas that are always true, such as $P\lor \neg P$
**Contradictions** - Formulas that are always false, such as $P\land \neg P$

Say $T$ is a tautology, and $C$ is a contradiction. Then:
**Tautology Laws**
- $P\land T  \equiv P$
- $P\lor T  \equiv T$
- $\neg T \equiv C$ 

**Contradiction Laws**
- $P\lor C  \equiv P$
- $P\land C  \equiv C$
- $\neg C \equiv T$


