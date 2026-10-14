**References**
- [PPT](https://edunexcontentprodhot.blob.core.windows.net/edunex/nullfile/1770827981918_IF3270-Mgg1b2b-Ensemble-Methods?sv=2024-11-04&spr=https&st=2026-02-11T16%3A39%3A41Z&se=2028-02-11T16%3A39%3A41Z&sr=b&sp=r&sig=IqyuaTCEoDTfcmBjknq4xVsN5nEEwc8bWrXp1YQYJnU%3D&rsct=application%2Fpdf)
# Why Ensemble Methods?
Ensemble methids have been very succesful on **structured data**. Specifically algorithms like *gradient boosting*, *XGBoost*, or *Random Forest*.

**The Wisdom of Crowds**
Sometimes the collective wisdom of many people can outperform the wisdom of a single expert. This is the core of ensemble methods.

**Secrets to success of ensemble methods**
- Ensemble Diversity
- Model Aggregation

# Concepts
## Terminology
- Base models: individual models
- Parallel vs Sequential: train each model independently vs sequentially in stages
- Homogenous vs Heterogenous: trained using the same vs different base-learning algorithms.

## Parallel Ensembles
- Bagging
- Boosting
- Stacking
### Homogenous Parallel
Same machine-learning algorithms (i.e. all have to use decision trees), all models trained concurrently.

We have a single data set, how do we obtain different base models with the same learning algorithms?

**Bagging - Bootstrap Aggregating**
**Bootstrap Sampling**
Take random data items into a 'bag', some objects may not be selected even once, these are called OOBs (out of bags). Out of bags can be useful as validation samples.

*"Exams should not use problems that were already used in the quizzes"*

Because different bootstrap samples will contain different examples repeating a different number of times, each base estimator will turn out to be somewhat different from the others.

## Random Forest
An ensemble of randomized decision trees usind a special extension of bagging.

**Randomized Tree**
Instead of data items, randomly sample features to combat dominant features that is repeatedly used in regular bagging.

Bootstrap Sampling + Randomized Tree = Random Forest.

After building the tree, we aggregate the classifying results we then use "majority voting".
![[Pasted image 20260212094647.png|500]]
Where blue is the correct class.
Randm forests are well suited for medium to large datasets

**Random Forest: d >> n**
When the number of independent variables (d) is larger than observations (n), regressions will not run. Random forests works because not all predictor variables are used at once.


### Heterogenous Parallels
Don't have to use just one algorithms (can be decision tree while others use regression).

**Heterogenous Ensembles with Weighting**
All base estimators have equal weight by default, but you can adjust, the final prediction is made by majority voting.
![[Pasted image 20260212095547.png|500]]

**Heterogenous Ensembles with Meta Learning**
With Stacking (read more)

Layer Stacking

## Sequential Ensembles