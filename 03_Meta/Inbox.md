

## Release Engineering
- Push/Pull Model
- Pull is better -> why?

# Math Tricks
- Ceiling Integer Division $\left\lceil  \frac{a}{b} \right\rceil=\frac{a+b-1}{b}$
- 

# CPP Tricks
- 7 + '0' = '7'
- Flat monotonic array: P = pN + t (unique)


# Math Concepts
- Chebyshev Sum Inequality
	- Proving greedy for dot product maximization
	$$N \sum_{i=1}^N a_i b_i \ge \left( \sum_{i=1}^N a_i \right) \left( \sum_{i=1}^N b_i \right)$$
	- Implication: pairing large elements with large maximizes, pairing large with small minimizes the sum.
	- Tips: no need to memorize it, it's quite intuitive.
	- Related:
		- Rearrangement Inequality
		- Given to ordered sequences of number, pairing in the same direction gives maximum sum, pairing in the opposite direction minimizes it.
	- Example Problem: [INC2024-F](https://tlx.toki.id/problems/inc-2024/F)
- Exchange Argument 
	- 


# Machine Learning
## Zero-Shot Model
- No explicit training to perform a task or recognize data. 
- Relies on transfer learning to adjust task.
- Typical of a foundation model

## Knowledge Distillation
- A.K.A Teacher-Student framework. A lighter model is trained to mimic responses or behaviours of a larger model trained on larger and complex data.
- Used for faster inference, great for embedded or edge computing.

## Ablation
- Removal of a component in machine learning (features, layers, loss functions, etc.)
- Used to:
	- Determine component importance
	- Identify redundancies
	- Simplify models
	- 

## Computer Vision Structure
**Backbone**
- Main feature extractor, takes raw inputs, turns it into feature maps
**Neck**
- Intermediate modules 
**Head**
- Maps the refined results form neck and turn into predictions