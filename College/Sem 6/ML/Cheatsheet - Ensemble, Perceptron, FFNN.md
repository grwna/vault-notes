- Predicted class probabilities is mean predicted class probabilities
**Hard vs Soft Voting**
Hard - 100% confidence for all model -> take the majority
Soft - Take confidence into account
**If using weights**
Multiply each classification/prediction with the model's weight
Stacking is Parallelx3

**Heterogeneous Voting vs Stacking**
Stacking's aggregation model learns from the previous layer's model.

Sequential Ensembles are usually homogenous

**Proses AdaBoost ($t$ menunjukkan suatu weak learner, $i$ menunjukkan data point) Training**
- Initialize $D_{t}(i)$: distribusi bobot awal data **dengan rata** , selalu memenuhi $\sum_{i}D_{t}(i)=1$
- Latih weak learner yang dibobotkan oleh bobot data $D_{t}(i)$
- Hitung error ($\epsilon_{t}$): dimana FUN adalah fungsi benar/salah (returns 1: wrong, 0: right)
$$\epsilon_{t}=\sum_{i=1}D_{t}(i)\text{FUN}(h_{t}(x_{i})=y_{i})$$
- Hitung bobot model $\alpha_{t}$:  dimana 1/2 dapat digantikan dengan learning rate
$$\alpha_{t}=\frac{1}{2}\ln (\frac{1-\epsilon_{t}}{\epsilon_{t}})$$
- Update bobot data
	- Correct point: turunin bobot, salah: naikin (dinaikin karena masih salah, model berikutnya harus lebih mempelajari ini)
	- $w_{i,new}=w_{i,old} \cdot e^{\pm \alpha_{t}}$
	- Note: plus/minus ditentukan oleh benar/salah
- Repeat

**Adaboost Inference**
- Get predictions from every weak learner
- Apply model importance
- Sum all to get final sign for each data point ($h_{t}(x)$ is prediction of t weak learner)
$$Fin=\text{sign}(\sum_{t=1}\alpha_{t}\cdot h_{t}(x))$$

**Gradient Boosting Training**
"Try to guess the weight of an object, then see how much you missed (error), ask someone else to guess only that error. Do until almost perfect"
$F_{i}$ - prediksi
- Initial guess $F_{0}$ - usually average of all target values
- Calculate mistakes (residual) - $\text{Residual}_{i}=\text{Actual}_{i}-\text{Predicted}_{i}$
- Latih sebuah pohon, yang memprediksi error (bukan kelas/target)
- Update prediksi: $F_{new}(x)=F_{old}(x)+(\eta \cdot h_{t}(x))$
- Repeat

**Gradient Boosting Inference**
- Sum of every single tree's prediction
- Equivalent to the $F_{new}$ of the final tree.
$$\hat{y}=F_{0}+\eta \cdot h_{1}(x)+\eta \cdot h_{2}(x)+\dots +\eta \cdot h_{m}(x)$$
Output bisa dianggap sebagai input.
**Random Forest should use Averaging (soft voting)**
**Bagging should use Majority Vote**

Hitung Forward Propagation pake matrix aja, lebih cepat dan gampang

Pahami Sigmoid, ReLU, Linear (wtf)