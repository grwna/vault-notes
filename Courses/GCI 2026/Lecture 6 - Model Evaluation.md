# Keywords
- Types of Evaluation Metrics
- Classification Models:
	- Confusion Matrix
	- Accuracy
	- Recall
	- Precision
	- F-Value
	- ROC-AUC
- Regression Models:
	- Mean Squared Error
	- Root Mean Squared Error
	- Mean Absolute Error
	- Coefficient of Determination
	
"In this lecture I learned about different ways to evaluate models performance. Model evaluation is done before training for testing different hyperparameters as well as at the end to evaluate the result of the training. There are different types of evaluation metrics for both classification and regression models, like accuracy, F1 score, MSE, MAE, etc. It is important to choose the correct evaluation score according to the problem's case, as a high score can be misleading. "

# Review of Supervised Learning
- A good model does not overfit
- Requires choosing good hyperparameters before training
# Classification
- Different types and metrics for evaluation.
- Case study: disease diagnosis system with 99% Accuracy.
	- For imbalanced datasets, if the model predicts everything as the label with the most frequency, high accuracy will be achieved but with terrible generalization.
	- Note that most people are not sick with disease, so this is a classic example of imbalanced dataset
- Alternative: Confusion Matrix
- From confusion matrix you can calculate:
	- Accuracy
	- Recall (Sensitivity) $\frac{TP}{TP+FN}$
		- Out of all positive cases, how much did the model catch
		- Good for cases where missing positives (false negative) cause serious consequences
	- Precision $\frac{TP}{TP+FP}$
		- When the model says positive, how often is it right?
		- Good when false positive is costly
	- F1: $\frac{2}{\frac{1}{recall}+\frac{1}{precision}}$
		- F1 is high if both precision and recall is high
		- $2\times \frac{Precision \times Recall}{Precision+Recall}$ 

**Implementation**
- Using `sklearn.metrics` just use `eval_score_name(y_test, y_pred)`
- This works for any classification scores (evan ROC-AUC)
- For confusion matrix, it returns a matrix, and you can calculate the metrics (like precision, accuracy) by accessing the elements inside the matrix
- You can also use `model.predict_proba()` to get probabilities
Use this to use custom threshold
```python
y_probs = model.predict_proba(X_test)[:, 1]
threshold = 0.7
custom_preds = (y_probs >= threshold).astype(int)
```

**Model and Threshold**
- Classifications are the model's outputs put through a threshold function (often 0.5)
- This means evaluation scores are based on the output of Model + Threshold, not model alone
- Metric unaffected by threshold? **ROC & ROC-AUC**

## ROC-AUC
- Receiver Operating Characteristic
- Are Under Curve
![[Pasted image 20260527150451.png|500]]

For a calculation step by step of ROC-AUC, read: [lecture slides](https://drive.google.com/file/d/14A8eGwD_ZtrqdGBosBZK8lG1nWQr0b0Y/view?usp=sharing)
Or watch [lectue video](https://www.youtube.com/watch?v=x7LwlsjrWPU&list=PLiEF5y87wtyzpPhgBT96Ex4LnWeC0qzif&index=3) starting from 17:00.

**Ideal Classifier vs Random Guess**
![[Pasted image 20260527151048.png|500]]

**Implementation**
- `sklearn.metrics` have:
	- `roc_curve()`
	- `auc()`
	- `roc_auc_score()`


**Summary of Classification Scoring**
![[Pasted image 20260527151224.png|500]]
Most used metrics are:
- Recall
- Precision
- ROC-AUC


# Regression
- Calculating difference between actual and prediction

**Methods**
- MSE - calculate the mean of squared errors
	- Sensitive to outliers (square)
- RMSE - the square root of MSE
- MAE - mean absolute error
	- Less susceptible to outliers
- $R^2$, Coefficient of determination
	- Compares the model to a dumb baseline that always predicts the mean
	- As sensitive to outliers as MSE 
	- $1-\frac{\text{Squared Error}}{\text{Squared Deviation}}$
	- Squared deviation is the distance of data point's target to the baseline mean
		- $R^2=1$ - perfect fit 
		- $0<R^2<1$ - partial fit 
		- $R^2=0$ - baseline fit
		- $R^2<0$ - terrible fit

**Implementation**
- `sklearn.metrics`
	- `evaluation_score(y_test, y_pred)`
	- For RMSE: `np.sqrt(mse)`
- `mean_squared_error()`
- `mean_absolute_error()`
- `r2_score()`

**Summary**
![[Pasted image 20260527191954.png|500]]
Most used: MSE/RMSE, $R^2$

# Summary
**Concept**
- Use evaluation methods based on the goal of the problem, does it need to be correct at all time? is it sensitive to a single major mistake? etc.
- Use visualizations to understand.
**Code**
- `evaluation_score(y_test, y_pred)`
- `model.predict_proba()`