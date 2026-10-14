- Probabilistic Reasoning
- Bayes Rule
- Independence
- D-separation

- [[#Introduction to Probabilistic Reasoning System|Introduction to Probabilistic Reasoning System]]
- [[#Bayesian Network|Bayesian Network]]
	- [[#Bayesian Network#Bayes Rule|Bayes Rule]]
	- [[#Bayesian Network#Structure of Bayesian Network|Structure of Bayesian Network]]
	- [[#Bayesian Network#Independence|Independence]]
	- [[#Bayesian Network#Bayesian Network as Joint Probability Distribution|Bayesian Network as Joint Probability Distribution]]
- [[#Classification with Bayesian Network|Classification with Bayesian Network]]
	- [[#Classification with Bayesian Network#Inference|Inference]]
	- [[#Classification with Bayesian Network#Classification|Classification]]
- [[#Learning with Bayesian Network|Learning with Bayesian Network]]
	- [[#Learning with Bayesian Network#Parameter Estimation|Parameter Estimation]]
	- [[#Learning with Bayesian Network#Contructing BN Structure|Contructing BN Structure]]
- [[#Naive Bayes|Naive Bayes]]

# Introduction to Probabilistic Reasoning System
AI is just prediction machines. One way to predict is to evaluate probabilities, for exmaple using *Joint Probability Distribution*.  
![[Pasted image 20251213131402.png | 400]]
Tables like this can be used to calculate probabilities of a specific occurence. For example:
- $P(\text{toothace}) = 0.108+0.012+0.016+0.064=0.2$
- $P(\neg\text{cavity}\;\vert\;\text{toothache})=\frac{0.016+0.064}{0.2}=0.4$
 
> [!important]
> We say $P(A\;\vert\;B)$ (read probability of $A$ given $B$), to refer to the probabilities that $A$ happens, such that $B$ already happened. This basically restricts the universe of discourse, which originally is $U$ into $B$.
> 
> $$P(A\;\vert\;B) =\frac{P(A\cap B)}{P(B)}$$
> You can prove this by using the fact that $P(A)=\frac{N(A)}{N(U)}$, with $N$ equals count of outcomes. Note that the universe of discourse for *given* probabilities are not $U$.

# Bayesian Network
## Bayes Rule

>[!example] Bayesian Theorem
> $$P(A\;\vert\;B)=\frac{P(B\;\vert\;A)\cdot P(A)}{P(B)}$$
> This shows a relationship between probabilities with different directions. For example:
> - If a patient has cancer, 90% chance the test is positive
> - Now, if the test is positive, what are the chances that the patient ACTUALLY has cancer?

>[!example] Law of Total Probability
>Given conditions $A$ and $B$, the probability of $P(A)$ is the probability of $A$ is true and $B$ is true, and the probability of $A$ is true and $B$ is false, hence *total probability*.
>$$P(A)=P(A\cap B)+P(A\cap\neg B)$$

Joint probability distribution is expensive ($2^n$, where $n$ are unique variables). Bayesian Network **exploits independence**.
## Structure of Bayesian Network
Structure:
- Nodes (variables)
- Directed arc (relationship between variables)
- Numerical parameters 

Bayesian network still requires $2^n$ nodes, but it is cheaper with nodes than raw probability like JPD.

Each node will have the probability of the parent, lets say:
```
A --> B -- > C
      ^
      |
      D
```

Then C will need P(C|B) and P(C|$\neg$B). B requires both the normal and the negation of both parents.

## Independence
![[Pasted image 20251213134942.png|500]]
*Figure 1*
### Connections
- Serial `C -> B -> A`
- Diverging `C <- B -> A`
- Converging `C -> B <- A`

We can exploit independence characteristics of these connections to know probabilities:
- Serial and Diverging
	- Knowing C will tell us ALL about A (*dependent*)
	- However, if we know B, knowing C tells us nothing about A
	- This means C and A conditionally separated
	- **Why is this true?**, knowing B is more sufficient than knowing C. if we know B, C doesnt add any more information than what B already gives. This is illustrated in fig.1.
- Converging
	- Knowing C tells nothing about A (without knowing B)
	- Knowing B makes A and C dependent.
	
>[!tip]
> - *Ask LLMs to give examples for these*
> - Understand the network notation (what is the cause, and what is the effect)

Independence can greatly reduce the amount of probabilities that needs to be specified.
### D-Separation
Two variables are *d-separated* (independent), if all path connecting them are blocked. A path is blocked if there are an intermediate node $V$:
- Serial/Diverging and $V$ is known
- Converging and $V$ is not known

## Bayesian Network as Joint Probability Distribution
PPT Page 13, what if you want to calculate probability of some variabels (not all). For the variables not counted, calcualate ALL combinations of the probability   z1.
![[Pasted image 20251213143328.png|500]]
![[Pasted image 20251213143930.png|500]]
With $V_2$ being the negation of $V_{1}$.
*Go to PPT page 16 to see Holmes-Watson Icy Roads Example*

# Classification with Bayesian Network
*Example problem is given in page 21 regarding fish (target label is X)*
![[Pasted image 20251213152123.png|500]]
## Inference
Inference is the process of calculating posterior probability of Query ($Q$) given evidence of all variables ($e$). Uses chain rule.
 $$Target=P(Q\,\vert\,e)$$
 Inference is that which all variables are asked (to see relationships for all variables).
## Classification 
We want to determine class based on observed variables. We want to find the *Maximum A Posterior*.
If label $X$ has two values $X1$ and $X2$, then we need to compare $P(X1\;\vert\;e)$ vs $P(X2\;\vert\;e)$.

In the example above, say, we need to calculate the chain rule probability of $P(x_{y},a,b_{2},c_{1},d)$ with $y\in \{1,2  \}$. Since our condition only gives $b_{2}$ and $c_{1}$, we have to calculate all probability (*total probability*) for the $a$ and $d$ (see page 25 for a clearer example). 

>[!note] Role of $\alpha$
>$\alpha$ is the normalization symbol, meaning the value next to it should be normalized

# Learning with Bayesian Network
Learning is the process of finding:
- Numerical parameters (base probability) 
- Structure (topology of the network, cause and effect)
Data is good at providing numbers
Humans is good at providing structure 

For Bayesian Network, the model has to learn from data. This is because learning from human experts are unreliable for estimating probabilities.

>[!note] Considerations
>- Variable ordering influences network structure

## Parameter Estimation
This is the step after the structure is complete, we need to fill the *conditional probability table* (CPT).
Here are the ways:
- Node without parent (Root Nodes)
	- $P(V_{i}=T)\approx \frac{\text{Occurence of }V_{i}=T}{\text{Total data}}$
- Node with parents $V_{j}\rightarrow V_{i}$
	- $P(V_{i}=T\;\vert\;V_{j}=T)\approx \frac{\text{Occurence of }V_{i}=T \text{ AND } V_{j}=T}{\text{Total data where }V_{j}=T}$
Where $V_{i}$ is the variable (node) and $T$ is the target's value.
  
> [!fail] Problem: Zero Occurence
> If a case has zero occurence, the probability is 0, which in the chain rule will cause the final value to be 0.
> 
>**Solution**: Laplace Smoothing (+1)
>Add 1 to the numerator and add 2 to the denominator

## Contructing BN Structure
**General Steps**:
1. Determine variable sets
2. Determine variable orders
3. Add nodes one by one while determining their parents

**Approaches**:
- Causal Knowledge: cause-effect logic
- Data-Driven
	- Check if P A given C = P C, if so A is not the parent of C
	- Check if P(C|A,B)=P(C|B), if so, A is not relevean if B is known
**Good orders** are `Cause -> Effect`
# Naive Bayes
Naive Bayes is a special case of bayesian network, one in which the *label* ($Y$) is a parent of every feature ($X$), and every features are independent. The graph looks like this:
![[Pasted image 20251213174758.png|250]]
This means with variables $A,B,C,D$, and label $Y$. 
$$P(Y,A,B,C,D)=P(X)\cdot P(A\vert X)\cdot P(B\vert X)\cdot P(C\vert X)\cdot P(D\vert X)$$
