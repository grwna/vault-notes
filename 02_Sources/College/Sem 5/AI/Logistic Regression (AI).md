# Keywords
- Linear Classifier
- Linear Discriminant Function
- $g(x)$
- Decision Rule
- Decision Surface
- Hyperplane
- Logistic/Sigmoid Function
- "Odds"
- "Log Odds" (Logit)
- Logistic Regression Coefficient
- Stochastic Gradient Ascent
- Epoch

# What
**Problem**: regression works for continuous value so it cant be used easily to classify data. 
**Solution:** make regression work for discrete values, these are the approaches:
1. Discretization - Linear regression + threshold (a.k.a **Linear Classifier**), this approach is flawed.
	- Sensitive to outliers
	The method used here is using a linear function (ex. $\hat{y}=1.33+0.33x$), then the result of that is compared to the threshold.

>[!important]
>The threshold used in our topics will always be 0.5

2.  **LDM** & Hyperplane
	A linear combination of the components of x.
	Data with $D$ length feature:
	$g(x)=w_{0}x_{0}+w_{1}x_{1}+\dots+w_{d}x_{d}=w^Tx$
	**Discriminant function:**
	$$g(x)=w^Tx$$
	**Decision Rule**:
	![[Pasted image 20251116200541.png|350]]
	This creates a hyperplane decision surface.
	Example: threshold 0.5, if > 0.5 then yes, else no
	
3. **Logistic Regression** <-- This is our focus now

|                    | Linear Regression | Logistic Regression   |
| ------------------ | ----------------- | --------------------- |
| Response Variable  | Normal            | Binary                |
| Impact on variance | Constant variance | Non-constant variance |
| Method             | Least Squares     | Maximum Likelihood    |

Logistic regression estimates the **probability of classes**
Where $\hat{y}$ :  log odds for **odds of success** (the log of $P_{success}$ divided by $P_{failure}$)
$$\hat{y}=\log\left( \frac{p}{1-p} \right)=b^Tx$$
which means the probability that $y=1$ given $x,b$ is:
$$p=P(y=1|x,b)=\frac{1}{1+e^{-\hat{y}}}$$
This probability is then compared to the thresold (0.5 in our case)


# Stochastic Gradient Ascent (Learning)
![[Pasted image 20251116211513.png]]Stochastic Gradient Ascent is an optimization method that changes the coefficient values (with random approximation) to increase log likelihood based on a randomly chosen example at a time.

**Stochastic gradient** update of $b_j$ :
$$b_{j}=b_{j-1}+\eta(y_{i}-p_{i})x_{ij}$$
Where:
- $\eta$ is learning rate
- $b_{j-1}$ is the previous iteration
- $(y_{i}-p_{i})x_{ij}$ is the error value

**Algorithm Steps**
Requires three input:
- $D$ - training data
- $T$ - max iterations
- $\eta$ - learning rate

**Steps**
- Initialize **b** values ($b_{i}$ for $i$ in [0, length of D])
- For $T$ iterations, do:
	- Randomly choose $d\in D$
	- Calculate probability $p_i$ using the **sigmoid function**
	- Then update **b** values
- Finally, return **b**

Each iterations are usually called **epochs**

Example:
![[Pasted image 20251116212858.png|300]]

>[!note]
>b0 is always multiplied with 1 for the $x_{ij}$. This is a dummy weight (1 is bias).

**Prediction Step**
After calculating $b$, use it in the sigmoid function like this here:
![[Pasted image 20251116214038.png|500]]