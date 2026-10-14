**References**
- [PPT](https://edunexcontentprodhot.blob.core.windows.net/edunex/nullfile/1770827981918_IF3270-Mgg1b2b-Ensemble-Methods?sv=2024-11-04&spr=https&st=2026-02-11T16%3A39%3A41Z&se=2028-02-11T16%3A39%3A41Z&sr=b&sp=r&sig=IqyuaTCEoDTfcmBjknq4xVsN5nEEwc8bWrXp1YQYJnU%3D&rsct=application%2Fpdf)

**Heterogenous Ensembles with Weigthing: Accuracy Weighting**
**Heterogenous Ensembles with Weigthing: Prediction**
Gets individual prediction from estimators/classifiers, then each pred value will be the weights.
Two Ways: hard and soft voting.
**Hard Voting (proba=False)**
round(clf1.val * class1 + clf2.val * class2) where:
- clf = classifier
- class = classes from classifier

# Boosting
Aim to combine several weak learners into a single strong learner.
Weak learner = only slightly better than random guessing.

## Adaptive Boosting
AdaBoost fixes the mistakes made by previous base estimator at every iteration.
 Computer model weight $a_{i}$. 
$$a_{i}=\frac{1}{2}\log(\frac{1-e_{i}}{e_{i}})$$
Where $e_{i}$ is error.

## Gradient Boosting
In AdaBoost, misclassified examples have larger weights.
In gradient boosting, misclassified examples have larger residuals, or loss gradients.

Each iteration aditively updates the current model with nes approximate weak gradient estimate.