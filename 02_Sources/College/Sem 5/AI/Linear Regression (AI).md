 # Keywords
- Dependent vs Independent Variables
- Simple Linear Regression (SLR)
- Intercept ($\beta_{0}$) and Slope ($\beta_{1}$)
- Multivariate Linear Regression (MLR)
- Parameter estimation
- Least Square Estimator (LSE)
- Regression --> Supervised Learning
- Hypothesis ($h$)
- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Residual Sum of Squares (RSS/SSE)
- R2-Score
- Cost Function $J(\theta)$
- Analytic vs Iterative Solution


# What
A way to predict output based on inputs. Assumes that the input and output has a **linear relationship**:
- Dependent ($y$) - output
- Independent ($x$) - input

**SLR**
Only one $x$ (input).

**MLR**
Multiple inputs ($x$)

# Least Square Estimator
Minimize SSE
$$SSE=\sum_{i=1}^ne_{i}^2$$
$$SSE=\sum_{i=1}^n(y_{i}-\hat{y}_{i})^2$$
$$SSE=\sum_{i=1}^n(y_{i}-b_{0}-b_{1}x_{i})^2$$
# Regression For Supervised Learning
1. **Training**: give labeled data to LSE formula
2. **Learning**: LSE calculates and results in hypothesis (ex. $h(x)=124.41+39.2x$)
3. **Prediction**: $h$ is then used to predict $y$ values on new data.

# Model Evaluation
After **training**, we can evaluate the model's performance by using several measures:
1. MAE
$$MAE=\frac{1}{n}\sum|y_{i}-\hat{y}_{i}|$$
2. MSE
$$MSE=\frac{1}{n}\sum(y_{i}-\hat{y}_{i})^2$$

3. R2-Score
$$R2=1-\frac{\sum(y_{i}-\hat{y}_{i})^2}{\sum(y_{i}-\overline{y})^2}$$

# Summary of LSE
- **Hypothesis** ($h$): Linear Function $h_{\theta}(x)=\theta^T\cdot x$
- **Cost Function** $J(\theta)$ : the function that we want to minimize. For LSE, $J(\theta)=SSE$ 
- **Goal** : find $\theta$ such that $J(\theta)$ is minimal.
- **Solutions**
	- **Analytic**: Find $\theta$ by deriving 
	- **Iterative**: if not found using analytic, use numeric methods like ***gradient descent***.

