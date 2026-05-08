- Unsupervised Learning
- Centroid
- WCSS
- Squared-error (K-means)
- DBScan
- Silhouette
- Purity

- [[#What & Why?|What & Why?]]
	- [[#What & Why?#What|What]]
	- [[#What & Why?#Why?|Why?]]
	- [[#What & Why?#Steps in Clustering|Steps in Clustering]]
	- [[#What & Why?#Representation of Clusters|Representation of Clusters]]
	- [[#What & Why?#Categories of Clustering Methods|Categories of Clustering Methods]]
- [[#Partitional Clustering: K-means|Partitional Clustering: K-means]]
	- [[#Partitional Clustering: K-means#K-means|K-means]]
	- [[#Partitional Clustering: K-means#Weakness of K-means|Weakness of K-means]]
	- [[#Partitional Clustering: K-means#Elbow Method|Elbow Method]]
- [[#Density-based Clustering|Density-based Clustering]]
	- [[#Density-based Clustering#DBSCAN|DBSCAN]]
- [[#Clustering Evaluation|Clustering Evaluation]]
	- [[#Clustering Evaluation#Internal Measures|Internal Measures]]
	- [[#Clustering Evaluation#External Measures|External Measures]]
	- [[#Clustering Evaluation#When to Use|When to Use]]

# What & Why?
## What
Clustering is grouping data to *clusters* based on similarities
![[Pasted image 20251213205546.png|400]]

**Finding Natural Groups**
Desirable Characteristics:
- High intra-cluster similarity (as close as possible)
- Low inet-cluster similarity (as far as possible)
- Similarity metrics has to be clear and has practical semantics based on domain

## Why?
Clustering is very important since most data we encounter is raw:
- Search engine results are clustered

## Steps in Clustering
**Main Steps**
- Feature selection: choosing subset of features
- Feature extraction: transformation into new features
- Similarity measure
- Grouping
**Optional Steps**
- Data abstraction
- Assessment of output
Clustering output: hard or soft

## Representation of Clusters
Clusters can be represented by:
- The *centroid* or it can also be represented by a *set of distant points*.
- Classification Tree
- Conjunctive Statements
- *For more details see page 15-16*

## Categories of Clustering Methods

![[Pasted image 20251213210918.png|600]]

1. **Partitioning Based**
	Identify partitions that optimize grouping criteria (*squared error*, *absolute error*).
	K-partition data construction; k $\leq$ data size.

2. **Hierarchical Based**
	Results in several nested partitions
	- Agglomerative: bottom up, merge
	- Divisive: top-down, split
	
3. **Density Based**
	Density: object count (how many objects)
4. **Grid Based**
	Uses grid structures.
5. **Model Based**

# Partitional Clustering: K-means
**Objective Criteria**: similarity within a cluster is *greater* than objects in other clusters.
**Iterative Relocation**: Iterative process of moving objects to clusters to improve partitions

An example of partition clustering is K-means (*Squared-error clustering*)

## K-means
1. Initialization
	- Define random k seeds as k clusters initial centroids
2. Iteration
	- Assign every instance from training data to closest centroids, form k cluster
	- Specify new centroid of each cluster
	- Stop conditions: convergence, thresholds, or max iterations (example: centroid no longer moves beyond a threshold distance)

*The K-means algorithm is explained in page 25*
*An example is given starting in page 26* 
**NOTE**: centroids are the point with the mean of every attributes

## Weakness of K-means
- How to choose value of $k$? (one solution is the *elbow method*)
- Initial Centroid Choice determines the final clusters. 
	- Often stops at local optimum
	- Final results are not stable
- Algorithm is not scalable
- Mean is defined only for numeric (one solution for nominal attributes is *k-modes*)
- Sensitive to outliers, since mean is calculated

## Elbow Method
How do we find the best $K$?

**Within-Cluster-Sum-of-Squares**
$$WCSS=\sum^n_{k}\sum^m_{i}||d_{i}-C_{k}||^2$$
We want a small WCSS, but if we go for the smallest, we can get WCSS = 0, where $K=N$. This is useless. 
**Solution**: find the perfect point where WCSS doesnt get lower significantly --> Elbow Point
![[Pasted image 20251213221615.png|400]]

>[!important] Notes on K-means Scalability
>If complexity of K-means is $O(nkt)$, why is it not scalable?


# Density-based Clustering
Clusters are dense regions in the data space, separated by regions of lower object density.
A cluster is the maximal set of density-connected points:
$$N_{\epsilon }(p)=\{ q\;\vert\;d(p,q)\leq \epsilon  \}$$
Where $N_{\epsilon }$ denotes neighbours.

![[Pasted image 20251213224042.png]]

> [!info] Terms
> - $\epsilon$ - radius of circle around a point
> - MinPts - minimum required neighbours in a circle to cound as *dense*

## DBSCAN
**Density Based Spatial Clustering of Applications with Noise**
Steps:
- Arbitrarily pick $p$:
	- If $p$ is a core point (it has MinPts neighbours within its $\epsilon$), this point becomes a cluster, and its neighbours will grab their neighbours, causing a chain reaction to grow the cluster.
	- If $p$ is a border point (not enough MinPts, no points are density-reachable), mark it, then find other $p$
	
> [!note]
>*Directly Density-reachable* - self explanatory
>
> *Density-reachable* -  means two points can reach by the chain reactions of their neighbours or directly. This can be asymmetric if one of the points is a border point (can't reach).
>
> *Density-connected* - two points have an object in between that makes them connected. This is guaranteed symmetric.

The data that do not belong to *any cluster* is called *noise point* or *outlier point*.

# Clustering Evaluation
## Internal Measures
Used when external label class does not exist.

**Two Pillars of Internal Quality**
- Cohesion - WCSS/SSE (smaller is better)
- Separation - BCSS (bigger is better)

**Silhouette Coefficient ($s$)**
Combines *cohesion* and *separation* for all data points $i$
$$s(i)=\frac{b(i)-a(i)}{max(a(i),b(i))}$$
Where:
- $a(i)$ - average distance of $i$ to all other points within the cluster (cohesion)
- $b(i)$ - average distance of $i$ to all other points in the nearest neighbour cluster (separation)

**Interpration of Values**
- Nearing +1 - cluster is very good
- Around 0 - overlapping, point is near border of two clusters
- Negative - misclustered, closer to neighbours than to own cluster

## External Measures
External class label exists.

**Purity**
Similar to calculating accuracy, this calculates:
- How much a cluster only contains data from only *one class*
$$Purity=\frac{1}{N}\sum^K_{k=1}max_{j}$$
Sum of members of class $j$ in $k$
- Pick majority class of each cluster
- Sum the members of the majority class for each clusters
- Divide by total data ($N$)

## When to Use 

| Condition           | Method                | Reason                                                         |
| ------------------- | --------------------- | -------------------------------------------------------------- |
| Real data/Wild data | Internal (Silhouette) | No label, just geometric shape                                 |
| Benchmark Data      | External (Purity)     | We have hidden labels, see if clustering can refind the labels |
| Choosing K          | Internal (Elbow)      | Find balance of intra-cluster variance                         |
