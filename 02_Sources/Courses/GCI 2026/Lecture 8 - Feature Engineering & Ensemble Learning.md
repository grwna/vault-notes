# Contents
- Overview of Feature Engineering
- Transforming Numerical Variables
- Transforming Categorical Variables
- Use of Domain Knowledge
- Ensembling

# Feature Engineering
## Concept
- Selecting, transforming, creating input variables to improve performance
- Supervised learning is just: $y=f(x)$. 
	- Make $x$ better
- Requires trial and error

**Types of FE**
- **Transforming**
	- Scaling, log-transformation
	- Encoding
- **Creating**
	- Combine existing features
	- Use domain knowledge to create new
- Extracting
	- Dimension Extraction (PCA, etc.)
- Selecting

Will focus on the bolded types.

**Variable Classification**
- Quantitative (Num)
	- Ratio Scale: Age, Weight
	- Interval Scale: Temperature (30 deg celcius is not 2x hotter than 15 deg)
- Qualitative (Cat)
	- Ordinal Scale: order
	- Nominal Scale: distinct
## Transforming Numerical Variables
- **Scaling**: Scaling values so calculations are not lopsided
	- Standardization: make mean 0 and std dev 1. 
		- $x_{std}=\frac{x-\mu_{x}}{\sigma_{x}}$
		- Good for: Outliers, Model assumes distribution
	- Normalization: make min 0 and max 1
		- $x_{norm}=\frac{x-x_{min}}{x_{max}-x_{min}}$
		- Good for: Algorithms with no distribution assumption
	- Non magnitude based models (like tree based)
- **Log Transformation**
	- Compress large values, makes relationships between variables easier to capture by model
	- Good for skewed data (lessens skewness)

**Code**
- `sklearn.preprocessing`
	- `StandardScaler`
		- `ss.fit_transform(X_train)`
		- Returns a numpy array
		- Have to convert to DF again to assign to a df
	- `MinMaxScaler`
	- `np.log(x)`

## Transforming Categorical Variables
- **Label Encoding**
	- Each category (unique values) is assigned as integer
	- Merit: simple
	- Demerit: may create fake ordering confusion
- **One-hot Encoding**
	- Each category becomes its own column, assigned with 1 or 0 
	- Merit: removes fake relationship
	- Demerit: high memory consumption
- **Cross Features** <- This one falls under creating
	- Create a new feature from a product of other features
	- Example: room area, from width and length
	- Merits: captures relationship that models cannot
	- Demerits: memory consumption, overfitting

**Code**
- `LabelEncoder`
- `pd.get_dummies(df, columns=[], prefix="").astype(int)` <- one hot
- Cross feature is purely pandas operations.  Or:
	- `PolynomialFeatures(degree=2, include_bias=True, interaction_only=True)`
	- Creates all pairwise products (`a, b, c` becomes `axb, axc, bxc`)
	- `degree` - polynomial degree
	- `interaction_only` - allow product with same feature or cross only


## Use of Domain Knowledge
- The biggest lever in feature engineering
- What affects house prices:
	- Basic: Size, Address, Age
	- Expert: Distance to schools, stations, malls, etc.
- Some techniques:
	- Merge rare values into one category


# Ensemble Learning
# Concept
- Combine multiple models to get majority vote or average
- Wisdom of the Crowds
- Types
	- **Bagging**
	- **Boosting**

## Bagging
- Bootstrap-Aggregate
	- Generate bootstrap resamples of training data
	- Train separate model with each resamples
	- Bagging mostly reduces variance, so base model with high-variance tend to benefit more
- Steps
	- Resample
	- Train
	- Repeat
	- Aggregate
- Core idea:
	- Diverse mistakes can cancel out
	- If everyone makes the same mistake: bagging wouldn't work

## Boosting
- Train weak model, then check incorrect predictions
- Reweight data -> give more weight to examples that were misclassified
- Repeat, then take average
- XGBoost, LightGBM -> the best
- Too many iterations can result in overfitting

**Code**
- `sklearn.ensemble`
- `BaggingClassifier(base_estimator=clf, n_estimators=n)`
- `GradientBoostingRegressor()`
- `XGBRegressor(n_estimators=n, eval_metric='rmse', early_stopping_rounds=m)`
	- Early stopping rounds fixes the overfitting problem

![[Pasted image 20260610163145.png]]