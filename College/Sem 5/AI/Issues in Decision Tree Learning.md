# Keywords
- Plurality-Value
- Overfitting
- Pre/Post-Pruning
- Tree Size
- Reduced Error Pruning
- C4.5
- Symmetric vs Asymmetric Binary
- Discretization
- Threshold
- Gain Ratio
- Costed Attributes
- Minimum Description Length Principle

# Issues in DTL
The main issues are:
- [[#Overfitting]]
- [[#Continuous-valued Attributes]]
- [[#Missing Values]]
- [[#Alternative Measures (Gain Ratio) |Alternative Measures]]
- [[#Differing Costs]]

## Overfitting
Result so good for training, but bad for overall data. The model memorizes too much of the data, making it bad at generalizing, especially when noises are present. 
In DTL, this is usually displayed by a long/complex tree with many branches (it is better to have simpler/smaller trees). 

So how to make simpler trees?
1. Pre-Prune
	Stop growing the tree before it becomes too complex
2. Post-Prune
	Let data be complex, then prune

|            | Pros                         | Cons                                                   |
| ---------- | ---------------------------- | ------------------------------------------------------ |
| Pre-Prune  | More direct                  | Difficult to determine when to stop growing the tree   |
| Post-Prune | More successfull in practice | Requires more steps (because it has to grow until fit) |
>[!note]
>Beyond the two pruning methods, the more important question is:
>"What criterion can we use to determine the final tree size with good enough accuracy?"

**Approaches to Determine the Final Tree Size**
1. Use **validation set**, which is separate from **training set** (ex. 2/3 training, 1/3 validation) to evaluate impacts of pruning
2. **Statistical test** on all training data to determine wether it is better to prune or keep a node
3. **Minimum Description Length**, measure of how small the tree can be without losing too much information. The formula is:
$$h_{MDL}=\text{argmin}_{h\in{H}}L_{c_{1}}(h)+L_{c_{2}}(D|h)$$
	Where,
	$L_{c1}(h)$: Length of hypothesis encoding (cost of tree's complexity)
	$L_{c2}(D|h)$: Length of data D given hypothesis h encoding (cost of tree's mistakes)
	argmin means "find the tree $h$ from all possible trees $H$, where the total cost is smaller than the others".

**Using Validation Set (Reduced Error Pruning)** 
Do until further pruning is harmful:
1. Evaluate impact on validation set of pruning each possible node
2. Greedily remove nodes, such that when it's removed, it improves the accuracy of validation set the most.
Good for large amount of data, so when separating the validation set, there is still a large amount to prune.

**For Small/Limited Data**
Use **C4.5** (improvement of ID3)
1. Grow tree until fit.
2. Convert resulting tree into equivalent set of `IF-THEN` rules for each path in tree
	Example: from [[Decision Tree Learning#What|tree shown in DTL]]
	- If `Outlook=Sunny` AND `Humidity=High` THEN `No`
	- If `Outlook=Sunny` AND `Humidity=Normal` THEN `Yes`
3. Prune (generalize) each rule by removing any preconditions that result in improving its estimated accuracy
4. Sort all the pruned rules by their accuracy, and consider the rules in this order when classifying future data instance.
	Example:
	- If `Humidity=High` THEN `No` -  acc = 95%
	- If `Outlook=Sunny` AND `Humidity=Normal` THEN `Yes` - acc = 92%

After pruning, the tree is not rebuilt, instead we use the rules as a decision list.

## Continuous-valued Attributes
**Discretization**
Uses threshold to create booleans:
Example:
Data = 0.1, 0.2, 0.3, 0.6, 0.7
Threshold = 0.5
The new values are: 
True If $d$ < 0.5 for $d\in{D}$,
False otherwise

**How to choose the threshold?**
![[Pasted image 20251116105224.png|400]]
You can choose it on boundary values where class changes, which gives two potential values:
C = (48+60)/2 = 54
C = (80+90)/2 = 85

Now use $Gain(S,A)$ for each potential breakpoint, and this can be done in tandem with calculating Gain for other attributes (each potential breakpoint acts as different attributes)

## Missing Values 
**Strategies**
- Assign it with most common value at node $n$.
- Assign it with most common value at node $n$ that have classifiation c(x).
- Assign it with every possible value of $A$, but with  probability for each values (used in C4.5.

When calculating the Gain, only consider the fraction with known values.
Example:
If |$D$| = 11 with 1 missing value in $A$, then the $Gain(S,A)$ is $\frac{10}{11}\cdot Gain(\acute{S},\acute{A})$.
Where $\acute{A}$ is $A$ without the missing value, and $\acute{S}$ is $S$ without the missing row.
![[Pasted image 20251116113611.png|400]]
For branching

**Missing Value as Separate Value**
Treat missing values as not missing, but as a special $?$ (`NULL`) value.
But not appropriate for cases where values are missing due to certain reasons.
Example: Field `isPregnant` for males, should be assigned as `NO`, not `?`.

## Alternative Measures (Gain Ratio)
There are other measures/metrics to help us **selecting attribute**
**Gain Ratio**
Scenario: 
For a date attribute, there will be many unique values (`Jan_31_2021` is different from `Jan_31_2022`). If we calculate the entropy, it will be very low, which gives **high gain**.
This makes it likely to be chosen, however we know **date** isnt actually a good attribute to generalize data.

$$GainRatio(S,A)\equiv \frac{Gain(S,A)}{SplitInformation(S,A)}$$
$$SplitInformation(S,A)\equiv-\sum_{i=1}^{c}\frac{|S_{i}|}{|S|}\text{log}_{2}\frac{|S_{i}|}{|S|}$$
Where $S_i$ is subset of $S$ for which $A$ has value $v_i$
Split information is the measure of how many unique values an attribute has and how evenly they are distributed. Think of it as the **entropy** of the values of an attribute, not the entropy in regards to the class.

Example:
![[Pasted image 20251116115604.png|400]]

**Special Case**
![[Pasted image 20251116115715.png| 500]]

## Differing Costs
**Approaches**
Tan and Schlimmer (1990):
$$\frac{(Gain(S,A))^2}{Cost(A)}$$

Nunez (1988):
$$\frac{2^{Gain(S,A)}-1}{(Cost(A)+1)^w}$$
Where $w\in [0,1]$ is the importance of cost.