# Keywords
- Confusion Matrix
- True/False, Positive/Negative
- Accuracy
- Precision
- Recall

# What
After training a **supervised learning** model, we need a way to measure how good it is.
We do this by comparing our model's prediction with reality from testing data.

# Confusion Matrix
The best way to visualize model's performance is with confusion matrix:

|                   | Prediciton: Positive | Prediction: Negative |
| ----------------- | -------------------- | -------------------- |
| Reality: Positive | True Positive        | False Negative       |
| Reality: Negative | False Positive       | True Negative        |
# Performance Metrics
1. **Accuracy**
	Total correct predictiokn vs total data tested.
	$Accuracy = \frac{TP+TN}{TP+TN+FP+FN}$
	
2. **Precision**
	How many predicted **positive values** are **actually positives**? The percentage of true positives.
	$Precision = \frac{TP}{TP+FP}$
	Used when the cost of False Positives are high (spam email filtering)
	
3. **Recall**
	From all instances that should be positives, how many are found?. Called recall because of all the **actual positives** , how many positives are retrieved/predicted?.
	$Recall = \frac{TP}{TP+FN}$
	If False Negatives are costly (medical)

SIngkatnya, 
- Precision are True positives, compared to predicted positives
- Recall are True positives, compared to actual positives

4. **F1-Score**
	Harmonic mean of Precision and Recall, used to find balance between the two metrics.
	$F1=2\times \frac{Precision \times Recall}{Precision+Recall}$ 
	F1 is the goto metric for:
	- Imbalanced dataset
		From 10000 dataset, about 99.5% are negatives. If the model predicts that ALL of the data are negatives, then it will have an **accuracy** of 99.5%. This isnt helpful since the positives arent detected. But the recall will be 0, which makes F1 a better measure. 
	- If False Positives are equally costly as False Negatives

# Classification for Multiclasses
The metrics we talked about so far is used for binary (positive/negative), how about when theres more than two classes?