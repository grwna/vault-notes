# Keywords
- ID3 Algorithm
- Best Attribute
- Entropy
- Information Gain
- Root

# Variable (Attribute) Types

## Quantitatives
**Numeric**
Quantitative values (measurable quantity) with Integer or Real representation.
Divided further to:
- Interval Scaled
	- Equal sized units, have orders. 
	- Example: dates (distance from 2012 to 2013 is same as 2013 to 2014). 
	- But we cant use ratios: 10 celcius is not twice as warm as 5 celcisus.
	- No zero point: The year 0 is not an empty value.
- Ratio-Scaled
	- Examples: weight, word count, years of experience.
	- Opposites of interval scaled characteristics

## Qualitatives
**Nominal/Categorical**
- Symbol or name of things (can still be numbers)
- Do not have meaningful order

**Binary**
- Equally valuable and carry the same weight
- Examples: male, female

**Ordinal**
- Like categorical but have meaningful order
- Magnitude between the orders is not known
- Examples: star rating (1 stars to 5 stars)

Other types include: **discrete** & **continuous**

# What, Why, When DTL
## What
- Method for Approximating discrete-valued target functions
- Represented by **decision tree**
	- Each internal node represents test of an attributes
	- Branch descending from a node corresponds to one possible value 
	- The values are represented **only** on the arc, not on nodes.
	- Leaf nodes represents classification results
	Example:
	![[Pasted image 20251115131032.png | 400]]
	
## Why
- Robust to noisy data
- Capable of learning **disjunctive expression**

## When
- Instances are represented by attribute-value pairs
	- Can also be used for continuous attributes if **discretized**
- Target function has discrete output values
- Disjunctive descriptions/representations is required for target
- Errors in training data (noises)
- Training data contains missing attribute values
These issues will be explored in [[Issues in Decision Tree Learning]] 

# ID3 Algorithm
A basic algorithm for DTL is ID3 (Iterative Dichotomiser 3, `3rd version`) uses **Top-Down** and **Greedy** approach.
 - Top-Down, root to leaf
 - Greedy, choose 'best' attribute as root

**Steps**
Start from root
1. Find the best attribute (e.g. $A$) for next node by calculating [[#Information Gain]].
2. Make $A$ as decision node
3. Make branches for each unique values of the attribute
4. Compare the class of training data to each unique values. 
	For example: `Outlook = sunny` has 3 yes class and 1 no class.
5. Repeat recursively until the stopping condition is reached for every branches

>[!note]
>Not all attributes have to be accounted in the tree, just the 'best' ones that may reach stopping conditions early. This is why **best attributes** are chosen, so as to not have a long tree.

![[Pasted image 20251115134036.png | 400]]
ID3 Flow Diagram

**Stopping Condition**
- After sorting, all data has the same classes (ex. 3 yes, 0 no. 4 no, 0 yes)
- No attributes left, take majority class of current branch (`PLURALITY-VALUE`)
- No example data for current branch, take majority class of parent
# Information Gain
**Entropy(S)**
Say $S =$ set of training examples
$Entropy(S)=$ minimum number of bits of information needed to **encode classification** of an arbitrary member of $S$.
Encoding classification: When we take random data in $S$, we can tell what class those data are.

$$ Entropy(S)\equiv\sum_{i=1}^{c}-p_{i}\log_{2}p_{i}$$
Where:
$S$: set of training examples
$c$: number of classes
$p$: proportion of S belonging to class $i$ (0 to 1)

Lower entropy: **low uncertainty**.

In regards to DTL, to get the "best" attribute means to get the most information gain. 

**Gain(S,A)**
$$Gain(S,A)\equiv Entropy(S)-Entropy(children)$$
Where 
$$Entropy(children)=\sum_{v_{A}}P(v)\cdot E(v)$$
Where:
$v_{A}$: represents one of the child nodes of attribute $A$(ex. `Outlook=Sunny` or `Outlook=Rainy`)
$E(v)$: Entropy of the child node $v$
$P(v)$: Proportion of data that went into child node $v$

Example Calculation:
![[Pasted image 20251115171319.png | 400]]

>[!note]
>Proportion is always calculated agains the **total** data

After you found a gain for one attribute, lets say Outlook. Then you need to determine best attribute next, specifically for `Outlook=Sunny`. The process is the exact same, but you dont calculate for **total data ($S$)**, you only factor in instances in $S$ where `Outlook=Sunny`.