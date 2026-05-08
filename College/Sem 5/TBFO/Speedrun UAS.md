Steps: 
- New Stack = $\epsilon$ - POP
- New Stack = Old Top + new symbol - PUSH
- Input = Old Top - Stack doesn't change

Acceptance:
- By final state
- By empty stack

# Recursive Descent Parser
Validate a string using a parse tree, based on the rules/production that it has

# Simplification of CFG
Three steps:
- Remove useless symbols
	- Non-generating
	- Unreacheable
- Remove unit production
	- Any Production rule in the form $A\to B, \text{ where } A,B \in \text{non terminals}$
	- Replace it using transitive properties
	- Production in the form $A\to B\;\vert\ a$, counts as unit production
- Remove null production
	- This is the most non simple one, practice again
	- [Neso Video](https://www.youtube.com/watch?v=mlXYQ8ug2v4&list=PLJmSDl6XULOMry0Gc5liKXaFFQZ3Mql6b&index=3)

**Chomsky Normal Form**
Only two forms:
- $A\to a$
- $A\to BC$
That is to say, two variables or one terminal (exactly)

**CFG to PDA**
If non-terminal
- Match top of stack to a rule
- Pop stack
- Push right hand side of rule onto stack
If terminal
- Match it with the input
- Pop the terminal
- Advance the input

**PDA to CFG**
Characteristics:
- There will be a non-terminal for every pair of states
- The starting non terminal will be the pair of states - (start state, finish state)
First we simplify the PDA
- Should only have one final state
- Should empty its stack before reaching final state
- Make each transition only POP or PUSH
	- That is, if they do both, then break it down into multiple states, using epsilons
	- What if it doesn't do either?
		- Create a dummy simbol that gets pushed then immediately popped
- Start with an empty stack and finish with an empty stack
	- Don't pop an empty stack
	- Don't push a full stack

The next step is the main process:
1. Setup S -> q,Z0,q or q,Z0,p
2. Pop transitions:
	- Transition is: read input x, then pop and not push anything
	- Right hand side of the variable is the input (x)
	- New Rule: [p, X, q] -> x
3. Push transitions:
	- Transition is: pop one symbol, push two back
	- Let's say the original stack top is X, and the pushed symbols are Y and Z
	- Then to clear X, you have to read the input, then clear Y to get the "middle" state, then clear Z to get the "end" state
	- **CFG Rule Pattern:** $[p, X, End] \rightarrow a[r, Y, Mid][Mid, Z, End]$
	- Get all possible combinations:
		- $[p, X, q_0] \rightarrow a[r, Y, q_0][q_0, Z, q_0]$
		- $[p, X, q_0] \rightarrow a[r, Y, q_1][q_1, Z, q_0]$
		- $[p, X, q_1] \rightarrow a[r, Y, q_0][q_0, Z, q_1]$
		- $[p, X, q_1] \rightarrow a[r, Y, q_1][q_1, Z, q_1]$
- If the CFG is not simplified first, then there is a stay/replace step
	- Read the input symbol
	- Create a rule for every possible end state (there are two)
	- The rule will be in this form:
		- $[p, X, q] \rightarrow a[r, Y, q]$
		- Where:
			- p is the initial state
			- r is the new state
			- q is the final state (remember that if there are two states {q,p}, there will be two different final states created as the rule)


Practice this more.

# Properties of CFL

## Closure Properties of CFL
**Closed Operations**
If L1 and L2 are CFL, then these operations result in CFL
Standard
- Union -> $S\to S_{1}\;\vert\;S_{2}$
- Concat -> $S\to S_{1}S_{2}$
- Kleene Star -> $S\to S_{1}S|\epsilon$
- Union -> reverse every production's bodies
Substition
- Replace every terminal in one language with another language
Homomorphism
- Special case of substition where the terminals are replaced with strings, not languages
Inverse Homomorphism
- Finding all string w such that it is in L

**Unclosed Operations**
- Intersection (using $a^nb^nc^n$ it can be proven that this is not closed)
- Complement
- Set Difference

**Note:** the intersection of CFL with Regular languages are **closed**. We can use this to prove CFL membership instead of using pumping lemma

## Decision Properties of CFL
**Decidable**
There exists an algorithm to solve these problems
- Emptiness
- Membership
- Finiteness

**Undecidable**
There does not exist an algorithm to solve these problems
- Equivalence of two CFL
- Subsets (is one CFL the subset of another?)
- Disjointness
- Universality

# Cocke Younger Kasami
Algorithm to solve the membership problem.
Formula is
$X_{i,j} = X_{i,k} \cdot  X_{i+k,j-k}$
Where i is the row, k is the length, j is the total length

A string is accepted in a CFL if the Start symbol is included in the top of the CYK triangle.

# Turing Machine
IDs are written right to the left of the current symbol it is "over".

**Languages**
- Recursively Enumerable - TM will halt at final state (accepted)
- Recursively Decidable - TM will halt when it's accepted and rejected

**TM Variants**
These variants of TM have the same language power as regular TM
- Infinite tape
- Multi-tape
- Non-deterministic
- Multi-dimensional

**Church-Turing Thesis**
Hipothesis that says turing machine can solve any computation problems that can be solved.

- [x] Pushdown Automata
- [x] Normalizing CFG & Chomsky Normal Form
- [x] Turing Machine
- [x] Intermediate Code Generation
Practice more:
- [x] CFG and PDA equivalence - PDA to CFG is difficult
- [x] Properties of CFG
- [x] Cocke Younge Kasami

**Things to Practice**
- PDA design
- CFG design
- Instantaneous Description