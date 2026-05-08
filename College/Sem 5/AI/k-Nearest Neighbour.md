
# Keywords
- kNN distance
- Symbolic vs Numeric distance
- Hamming Distance
- Eucledian, Manhattan, Minkowski distance
- Curse of Dimensionality
- Feature Scaling
# What
A Supervised Learning algorithm. kNN is one of the most simple but powerful classification algorithm.

**Characteristics**
1. Instance-Based Classifier
	kNN does not make a generalized "model" or "hypothesis" during training. Instead it stores **ALL** data in memory.
2. Lazy Learner
	As mentioned before, during training it doesn "learn" much, instead it just stores data. The heavy computation is done later.
3. No Hyprothesis
	It writes no rules.

# Prediction Process
**Steps of kNN prediction**
1. Calculate distance - calculate the similarity of new data to all training data stored in memory. This is the most crucial step.
2. Find k-Nearest Neighbour - for a chosen **k**. Find k neighbours with the least distance (most similarity).
3. Pick majority class - from the "kNN", observe which class appears the most
4. Predict - the majority class will be chosen as the prediciton class for the new data

**Choosing k**
- Low k - more sensitive to **noise**
- High k - can be too smooth
- Usually k is odd to avoid tie

# Distance Measurement
Depends on data types:
- Symbolic Attribute (Categorical)
	- Example: `outlook` (Sunny, Overcast, Rainy)
	- Method: **Hamming Distance**
	- Distance = 1 if equal, Distance = 0 if not equal, for each attribute
	
- Numeric Attribute (Continuous)
	- **Eucledian Distance**
		$D_{e}=\sqrt{\sum{(p_{i}-q_{i})^2}}$
		Distance using pythagoras theorem

	- **Manhattan Distance**
		$D_{m}=\sum |p_{i}-q_{i}|$
		Raw distance (taxicab distance, cant cut corners)

	- **Minkowski Distance**
		Generalization of $D_{m}$ and $D_{e}$. Euclidean is Minkowski with $p=2$, Manhattan is Minkowski with $p=1$.
# Pros and Cons of kNN
**Pros**
- No need for complex assumption calculation of data shape
**Cons**
- Classification for new data can be expensive
- All features are taken into account. **Irrelevant features** included. This can be problematic if large distances are measured but only for irrelevant features.

**Curse of Dimensionality**
If data has many features (thousands for example), kNN will perform terribly.

**Feature Scaling**
This is the practice of **normalization distance** for numeric data with different scales. For example, age and wage, ages will be way lower than wages. This can impact distance calculation negatively.