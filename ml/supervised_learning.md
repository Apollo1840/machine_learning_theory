# Supervised learning methods

## Regression

### Linear regression
reference: 
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28ML.one%7Ce8b3e705-493c-431b-b04e-8e9e3752864d%2F04-linear%20regression%7Ccc20eaf9-d27f-4c5e-9886-f21dc3e987f8%2F%29&wdorigin=NavigationUrl
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2F%E7%BA%BF%E6%80%A7%E5%9B%9E%E5%BD%92%7Cd1449063-187d-41a7-93d4-c0f541144360%2F%29&wdorigin=NavigationUrl

#### Assumptions
- Linear: output is linearly dependent on the input variables.
- ( | ) Column: no linear correlation between the input variables.
- ( - ) Row: observations are i.d.d
- ( r ) Residuals are i.d.d as a normal distribution with the same variance.

#### Advance:
- Linear regression with AIC step
- Ridge regression; Lasson regression
- Robust regression

### Polynomial regression


## Classification
reference: 
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2F%E5%88%86%E7%B1%BB%E5%99%A8%E5%88%97%E4%B8%BE%7C5b7bac14-a960-4d72-97b4-5523537a9fe7%2F%29&wdorigin=NavigationUrl
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28ML.one%7Ce8b3e705-493c-431b-b04e-8e9e3752864d%2F01-Classification%7C9dbae856-01e1-45c3-b0dd-271fdcf88069%2F%29&wdorigin=NavigationUrl
  

Binary classifier to Multi-classifier
- OVR
- OVO

### Logistic regression
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2FLogistic%20regression%20and%20kernel%7C540a838d-7ab5-46ef-930f-fe5b537a0815%2F%29&wdorigin=NavigationUrl

### Decision tree (forest)
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28ML.one%7Ce8b3e705-493c-431b-b04e-8e9e3752864d%2FDecision%20Tree%28Forest%5C%29%7C3f9ac3ce-1461-4434-bddf-4eb1407368f7%2F%29&wdorigin=NavigationUrl

#### Process
- Choose split: choose a feature and a threshold to split the data
- Evaluate split: measure the quality of the split, determine whether split further or stop.
- Assign label: assign label to the final leaf node.

#### How to split

In brutal force, we calculate all impurity gain of different feature and split combination.

There are other tricks like:
- for feature:
  - use important features only
  - random subset (in RF)
- for split:
  - use binary search
  - chunklise 

#### Impurity measures
- Gini score: := $1 - \sum_{i=1}^{C} p_i^2$

- Entropy
- Missrate

Impurity gain: $I - (p * I(1) + q * I(2))$.

#### Post-Pruning 
Often on validation set. To reduce model complexity
- Reduced Error Pruning (REP): Iteratively removes nodes and checks validation accuracy.
- Cost Complexity Pruning (CCP): Measures the trade-off between tree complexity and error reduction.

#### Forest building
- Bagging: Each tree is trained on a different random subset of the data.
- Random: Random subset of features. (size = $\sqrt(d)$)
- Voting:  Uses majority voting across trees.

### SVM
reference: 
- https://www.youtube.com/watch?v=bM4_AstaBZo&ab_channel=ritvikmath
- https://www.youtube.com/watch?v=uV5TnFc7eaE&ab_channel=MachineLearningandAI

Intuition: maximize the margin between linear decision boundary line and 'support vectors'(closest to the linear decision boundary).

1) In hard margin case, to maximize margin, we solve:

$$
\min_{\mathbf{w}, b} \|\mathbf{w}\|
$$
$$
\text{s.t.} \quad y_i (\mathbf{w} \cdot \mathbf{x}_i - b) \geq 1, \quad \forall i = 1, \dots, N
$$

2) In soft margin case, we loosen the constraints to a penalty term of the target.

We got:

$$
\min_{\mathbf{w}, b} \lambda \|\mathbf{w}\| + \frac{1}{N} \sum_{i}{(1-\quad y_i (\mathbf{w} \cdot \mathbf{x}_i - b) )}
$$

Furthermore, we do not want successfully classified points contributes to the loss, so we apply **hinge loss** to deactivate them.

$$
\min_{\mathbf{w}, b} \lambda \|\mathbf{w}\| + \frac{1}{N} \sum_{i}{max(0, (1-\quad y_i (\mathbf{w} \cdot \mathbf{x}_i - b) ))}
$$

(PS. If you draw this loss function, it is an linear estimation of logistic regression loss. see: https://www.youtube.com/watch?v=uV5TnFc7eaE&ab_channel=MachineLearningandAI)

#### SVM dual
There is a dual problem of SVM problem(optimization) where only the inner product of support vectors are curioused.

#### SVM kernel

Kernel trick is a trick to quickly compute the inner product of up-projected vectors.

In SVM case, this trick is based on inner product of the original vectors.

In another word, we apply kernel function to the inner product of the original vectors and get the inner product of up-project vectors.

$$
f(x)^{T}f(y) = K(x^{T}y)
$$

#### SVM kernel II
In another aspect, we could use landmarks to up-project the points to distance-feature to those landmarks with gaussian function:

$$
f_i = \exp \left( -\frac{\|x - l^{(i)}\|^2}{2\sigma^2} \right)
$$

We can choose other data points as landmarks as:

$$
f_i = \exp \left( -\frac{\|x - x_{i}\|^2}{2\sigma^2} \right)
$$

We can also do not choose gaussian kernel, but polynomial kernel as:


$$
f_i = (x^{T}x_i + 1)^{2}
$$

### kNN
K-Nearest Neighbors (KNN) is machine learning algorithm used for both classification and regression tasks. It works based on the idea that similar data points are close to each other in the feature space.

- classification: the label of an instance is the majority of labels of its k neighbors.
- regression: the value of an input is the average value of its k neighbors.

disadvantage: too-strong assumption; memory and computationally intensive.

#### Distance

- For numericals: 
    - Minkowski Distance: L1(Manhattan), L2(Euclidean), L(inf)(Chebyshev)
    - Mahalanobis Distance. (considering correlation of features)
- For arrows: consine similarity
- For categoricals: hamming distance
- For sets: Jaccard distance

When mixed, how to transform categorical feature to numerical feature:
- One-hot encoding
- Label encoding (if ordinal)
- Target encoding (very tricky)

### NN (MLPClassifier: Multi-layer Perceptron)

### AdaBoosting




