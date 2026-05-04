# Finite Automata

![[finite_automata_example.png.png]]
## Structural Representations
Alternative ways of specifying a machine:
- Grammars
- Regexs

## Concepts
- **Alphabet**: finite nonempty set of symbols (noted as Σ)
- **Strings**: finite sequence of symbols, made up of alphabet Σ
- **Empty String** ($\epsilon$): The string with zero occurrences of symbols from Σ
- **Length of String** |w|: amounts of symbols in a string w
- **Powers of an Alphabet**: set of strings with length k, that contains symbols from Σ
- **Σ***=Σ0 U Σ1 U Σ2 U Σ3….
- **Positive Closure**, closure but without power of 0
- **Concatenation**: concat
- **Language**: L is language, if L is a subset of a closure of alphabets
- **Empty Language** Θ: language without strings, not even empty strings

# DFA & NFA
## Deterministic Finite Automata
### Definition
A DFA is a quintuple consisting of:
$$
A=(Q,\Sigma,\delta,q_{0},F)
$$
- $Q$ is a finite set of states
- $\Sigma$ is a finite alphabet
- $\delta$ is a transition function
- $q_{0} \in Q$ is the start state
- $F \subseteq Q$ is a **set** of final states
Example:
![[example_dfa.png]]

An FA accepts a string $w$ if there is a path in the transition diagram that
- Begints at $q_{0}$
- Ends at one of the $F$
- Has sequence which contains all of $x$ for $x \in w$

Currently as i explained it, the transition function ($\delta$) operates on a **single symbol**. This can be extended into $\hat{\delta}$ which operates on strings.

## Nondeterministic Finite Automata
### Definition
A DFA has **one** unique path for any inputs of strings. In contrast, an NFA can have many paths for any input string. For example, while in $q_{0}$, if you input the symbol **0**, you can either go back to $q_{0}$ or go to $q_{1}$.

Formally, an NFA is a quintuple, with the only difference from DFA being its transition function:
- $\delta$ is a transition function from $Q \times \Sigma$ to the powerset of $Q$

## Equivalence of DFA vs NFA
- NFA's are easier to program in
- NFA and DFA is equally powerful, meaning they both can understand the same language $L(D) = L(N)$
- This involves [subset construction](http://www.neil.dantam.name/csci-561/B05-subset.pdf). To convert from NFA to DFA.

Details of subset construction:
- $Q_{D}={S:S\subseteq Q_{N}}$
- $F_{D}={S\subseteq Q_{N}:S\cup F_{N}\neq 0}$
- ![[Pasted image 20250905005132.png | 200]]
