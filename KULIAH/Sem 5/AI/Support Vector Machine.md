# Keywords
- Binary Classification
- Linear Separability
- Linear Classifier
- Hyperplane Classifier

# What & Why
Good performance in various applications like bioinformatics, text classification, etc.

**Binary Classification**
Given a training data ($x_{i},y_{i}$), with $x\in \mathbb{R}^d$ and $y\in{-1,1}$, learn a classifier function $f(x)$, such that if the value of $f(x) \geq{0}$, then $y=+1$, and other wise $y=-1$.

**Linear Separability**
A linearly separable data is a data in which when plotted, the values of two classes can be clearly and completely separated using a **straigt line**. The larger the margin of the line is, the better.

**Linear Classifier**
The line that separates linearly separable data. A linear classifier has the form:
$$f(x)=w^\intercal x+b$$
In 2D the discriminant is a line: 
- $w$ - a normal to the line (know as the weight vector)
- $b$ - bias
- $\intercal$ - means transpose
In 3D, the discriminant is a plane, and in nD it is a hyperplane.

For a k-NN classifier, it is necessary to carry the training data
For a linear classifier, the training data is used to learn $w$, and then discarded. Only $w$ is needed for classifying new data.

**Perceptron's Weakness**
Biggest weakness of perceptron is that it will not find the same hyperplane every time.

**SVM Objective**
Find the optimal separating hyperplane which maximizes the margin of the training data.
Uses *quadratic optimization* to avoid local minimum that is present in *Neural Networks*.

**Hyperplane Classifier**
The size of a margin is equal to $\frac{2}{\lvert \lvert w \rvert \rvert}$, which means to optimize hyperplane we need to minimize $\lvert \lvert w \rvert \rvert$ while keeping concistencies with the data.

**Vector Direction**
![[Pasted image 20251127150502.png|600]]

# SVM for Linearly Separable Data
Source: [youtube](https://www.youtube.com/watch?v=RTcwgAlUwlo)
## Support Vectors
Two classes can be separated by a pair of linear separator. **Support Vectors** are Vectors in training data that *supports* the separators.

More specifically, support vectors are *data points* that lie closest to the decision surface (or hyperplane). They are the data points that are most difficult to classify, and have direct bearing on the optimum position of the separator.

Larger margins has better generalization, data close to the separator represents uncertainty in classification.

**Support Vectors** Satisfies $$\vert\vec{w}\cdot \vec{x_{i}} +b\vert=1$$ where $x_{i}$ is the i-th  support vector
And all data points in training data with labels "+" and "-" satisfies 
$$y_{i}(\vec{w}\cdot \vec{x_{i}} +b)\geq1$$
As stated in [[Support Vector Machine#What & Why|Hyperplane Classifier]], we need to minimize:
$$V(\vec{w}, b)=\frac{1}{2}\vec{w}\cdot \vec{w}$$
## Lagrangian Formula
An easier way to calculate the search for the optimal hyperplane.
![[Pasted image 20251127164837.png|500]]

>[!important]
>The magnitude of $\alpha_{i}$ indicates weight, or inflience of the data point $x_{i}$

But why do we only take non-zero alphas?
![[Pasted image 20251127172412.png]]

**Lagrangian Dual Problem**
![[Pasted image 20251127165357.png|400]]

To further simplify it (removed the dependence on $w$ and $b$)
![[Pasted image 20251127170243.png |400]]

## Quadratic Optimization Problem
![[Pasted image 20251127170820.png|400]]

**Quadratic Programming**
QP is the problem of optimizing a quadratic objective funciton and is one of the simplests form of non-linear programming.
![[Pasted image 20251127172639.png|300]]

The objective function can contain bilinear or up to second order polynomial terms, and the constraints are linear and can be both equalities and inequalities.

**Geometric Representation**
![[Pasted image 20251127183708.png|400]]
>[!important]
>Know the difference between separator plane, and boundary plane. The separator is the solid line while boundaries are the dotted lines.


**Example**
For the data:

| x1  | x2  | Class |
| --- | --- | ----- |
| 3   | 1   | +1    |
| 3   | -1  | +1    |
| 6   | 1   | +1    |
| 6   | -1  | +1    |
| 1   | 0   | -1    |
| 0   | 1   | -1    |
| 0   | -1  | -1    |
| -1  | 0   | -1    |
In order to get the alphas we can do this:
![[Pasted image 20251128091240.png|500]]

Remember that the support vectors are the closes to the separator (there should be a separator line at $x1 = 2$).

Also focus on:
$$f(\vec{x})=\sum_{i=1}^{nsv}(\alpha_{i}y_{i}\vec{x_{i}}\vec{x})+b \tag{1}$$
$nsv$ -  means iterate over all support vectors.
$\text{Everything with } i$ - things related to the support vector

Basically we want to operate each support vectors, which will operate it with all other support vectors (including itself), and simplify the equation to include only $\alpha$ and $b$. And then solve $\alpha_{i}$ and $b$.
![[Pasted image 20251128131515.png|400]]
Now that we have the values for $\alpha$ and $b$, substitute them into eq(1). Now you can use eq(1) to predict a data's class by plugging its value into the $\vec{x}$ (NOT $\vec{x_{i}}$)

NOTE: remember that $\alpha_{i}$ means the alpha for the $i$-th support vector (or any vectors, but the ones that will be used are support vectors's alpha)

>[!important] Difference of SVM by Hand and Program Implementation
> **SVM by Hand**
>- Identify support vectors visually 
>- Calculate alphas based on the support vectors
> 
> **Program Implementation**
> - Iterately solve the large **Dual Optimization Problem** to find the optimal set of $\alpha_{i}$, for every single training point.
> - Determine support vectors, which are the training points whose $\alpha_{i}$ is greater than **zero**

For doing by hand, it is much easier to use the primal form:
1. Calculate $w$ using:
$$w\cdot x+b=y$$
	Where $w=(w_{x},w_{y})$.
	Example: for point (1,6) --> $1w_{x}+6w_{y}+b=1$
	**Remember:** both $x$ and $w$ are vectors.
2. If you have multiple data points, you will have a *system of linear equations*, use this to find values for $w_{x}$ and $w_{y}$.
3. After getting those values, calculate the alphas using
$$w_{z}=\sum \alpha _{i}y_{i}x_{i}$$
	Where $z\in \{ x,y \}$, you will have a system of two equations.
	Then use the SVM constraint:
	$$\sum\alpha_{i}y_{i}=0$$
4. Solve the equations and you can get all the alphas.