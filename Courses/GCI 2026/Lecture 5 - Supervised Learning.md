Libraries:
- scipy
- sklearn

**Methods**
- Multiple regression 
- Logistic regression 
- Decision Trees
- kNN
- SVM

**Concepts**
- Explanatory variables -> features used as considerations for predicting labels
- Multicolinearity -> if two non label features are highly correlated with each other (>0.5), they might be multicolinear
	- This is a problem, and you have to pick one of the features, and drop the other.
- Overfitting ->memorized everything, even noise. (Keep simple)
- Overfitting Prevention:
	- Regularization
	- Cross-validation
	- Early stopping
	- Increase data
- Regularization -> Encourage simpler models, by penalizing large parameters, or other 
	- Penalty is added to the loss function
	- Ridge regression -> add L2 Norm Penalty (L2: Circle Contour)
	- Lasso Regression -> add L1 Norm Penalty (L1: Square Contour)
	- `sklearn.linear_model.Ridge`
	- `sklearn.linear_model.Lasso`
	


# Workflow
![[Pasted image 20260523000305.png|500]]
**Supervised Learning Workflow**

## Data Preprocessing
- If missing data count is small, removing rows should be fine.
- Feature selection: 
	- Forward selection, backward elimination
	-  stepwise selection, AIC, BIC <- Statistical methods
	- Use correlation to find what feature too use
-  Scaling/Standardization
	- `StandardScaler()`
	- `scaler.fit(X_train)`
	- `scaler.transform(X_train/X_test)` -> array/df
-  Encoding
	- Encodes non numerical values into a format understandable by models
	- OneHot -> Each unique value becomes it's own columns
	- Use `pd.get_dummies(data['columns'])` to do one hot encoding using pandas directly


**Model Building & Evaluation**
- Train-test split:
	-  `from sklearn.model_selection`
	- `train_test_split(X, y, test_size=, random_state=, stratify=)`
	- returns 4 dataframes (X, X', y, y')
	- Stratify ensures class distribution remains the same as original distribution.
- Train with `model.fit(X, y)`
- `model.score()` to see accuracy

**Evaluation Considerations**
- For imbalanced target, accuracy may not reflect the model performance well.
	- Use precision, AUC, recall, F1Score

# Improving Models
## Methods & Models
**Linear/Multiple Regression**
- Uses R^2 as score

**Logistic Regression**
- Change labels to binary variables or enum to be able to be predicted.
- For classification

**Decision Tree**
- Classification: `DecisionTreeClassifier()`
- Regression: `DecisionTreeRegressor()`
- Parameters are: `random_state`, `max_depth`, `criterion` which can be entropy, impurity, etc.

**kNN**

**SVM** 
- `sklearn.svm.LinearSVC`
- Benefits a lot from standardization

# Evaluating Models
- Data Splitting
	- Training set -> train
	- Validation set -> evaluate models while training
	- Test set -> evaluate best model
- Holdout Validation -> split data to train and test
- K-fold Cross-Validation 
	- Split data into K-splits/folds
	- Train K-times/iterations
	- At each iterations, the K-th fold is used as validation, and the remainder as training set
	- Take mean validation score from all iterations
- Stratified K-fold Cross-Validation -> K-fold cross-V with maintaining data distribution (stratify)
- Hyperparameters -> Find using Grid Search

**Coding the Evaluation**
Using K-fold Cross-Validation
- `sklearn.model_selection.cross_val_score`
- `cross_val_score(model, X, y, cv=fold_count)`
- Note: calling the function will run training, but it won't train the `model`
- This step is used only to test hyperparameters

**Hyperparameters**
- Hyperparameters are parameters set 'manually' before training
- How to find:
	- Grid Search -> can find optimal good, time consuming, use narrow grid to make lighter
		- `GridSearchCV(estimator=model, param_grid={dict of string:list}, cv=k)`
		- Uses stratified k-fold cross by default
		- Returns a *trained model* using the best hyperparameters