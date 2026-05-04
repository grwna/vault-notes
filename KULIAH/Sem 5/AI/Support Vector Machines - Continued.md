- Slack Variable
- Soft Margin
- C Parameter
- Dimension Transformation
- Kernel Trick
- RBF Kernel
- One-against-All
- One-against-One
- Voting
- DAGSVM
# SVM for Non-Linearly Separable Data
In real life, data is rarely linearly separable, this is due to:
- Data's natural characteristics
- Noise

Solutions for this problem are:
- Slack Variables (Soft Margin SVM)
- Non-Linear Boundary Transformation

## Slack Variables 
To handle noise, we loosened the constraint to allow some wrong classifications, or allow data to be inside the margin.
*Slack Variable* ($\xi_{i}$): non negative variables that measures how much a point violates a margin.
- $\xi_{i}=0$ - best, data is correctly classified and not inside margin
- $0<\xi_{i}\leq 1$ - data is correctly classified but inside margin
- $\xi_{i}>1$ - misclassification

Then we have a new minimization function:
$$\frac{1}{2}||w||^2+C\sum^N_{i=1}\xi_{i}$$
**Role of C (Regularization)**
C is user chosen constant to control trade-offs between wide margin and classification error (penalty)
- Big C - Less tolerant to $\xi$, model will work harder to corretly classify (narrow margin, can overfit, sensitive to noise)
- Small C - More tolerant to $\xi$  (Wide margin, can underfit, less sensitive to noise)


## Non-Linear Boundary Transformation
For non linear patterned data, straight lines can never separate it.
- **Main Idea** - mapping data in low dimensions to high dimensions using certain functions, such that a high dimension hyperplane can separate the data.
- **The Trick** - using the kernel trick, we do not need to actually map into high dimensions, we just need to calculate distances such that it seems like they are mapped into high dimensions.

## The Kernel Trick
As mentioned before, mapping data to high dimensions are expensive. So we use the kernel trick. 
SVM only requires dot product ($x_{i}\cdot x_{j}$), this dot product is for 2D, for higher dimensions, we generalize it as the kernel funcion $K(x_{i},x_{j})=\phi(x_{i}\cdot \phi(x_{j})$.

 **Types of Kernels**
- Linear Kernel
- Polynomial Kernel - good for curved boundaries data
- RBF - most common, infinite dimensions
- Sigmoid Kenrel


# SVM for Multi-Class
SVM is inherently a *binary classifier* in order to make it work as multi-class classifier, we need to breakdown the problem into multiple *binary classication* sub-problems.

## One-againts-All/Rest (OvA)
One *binary model* for each class, which seperates a specific class with *all other* classes.
For $k$ classes, we will build $k$ models.
- Model 1: Class A vs (B + C + D...)
- Model 2: Class B vs (A + C + D...)
- ...

**Decision**
New data is predicted by all models, the model with the highest function value will be the winner class (each model represents a specific class).
## One-againts-One (OvO)
Creates a *binary model* for each class pairs. We will train $\frac{k(k-1)}{2}$ (handshake formula) amount of models, where $k$ is the amount of *class*.

**Decision**
The decision is then made using a voting mechanism from each model. 
Note: there are no transitive properties for the votes

## DAGSVM
Similar to OvO, however the decision does not use voting, and instead uses a graph/tree structure for faster decision process ($k-1$, which is $O(k)$ compared to OvO which is $O(k^2)$.

**Decision**
Uses a tournament/elimination process
Example: A vs D
- If A wins, eliminate D, traverse to nodes for A vs other classes
- If D wins, elimiate A, ....




