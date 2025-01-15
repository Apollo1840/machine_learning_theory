# Supervised learning methods

## Regression

### Linear regression
reference: 
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28ML.one%7Ce8b3e705-493c-431b-b04e-8e9e3752864d%2F04-linear%20regression%7Ccc20eaf9-d27f-4c5e-9886-f21dc3e987f8%2F%29&wdorigin=NavigationUrl
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2F%E7%BA%BF%E6%80%A7%E5%9B%9E%E5%BD%92%7Cd1449063-187d-41a7-93d4-c0f541144360%2F%29&wdorigin=NavigationUrl

#### Assumptions


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

#### Impurity measures
- Gini score
- Entropy
- Missrate

#### Post-Pruning 
To reduce model complexity
- Reduced Error Pruning (REP): Iteratively removes nodes and checks validation accuracy.
- Cost Complexity Pruning (CCP): Measures the trade-off between tree complexity and error reduction.

### SVM
reference: https://www.youtube.com/watch?v=bM4_AstaBZo&ab_channel=ritvikmath

Intuition: maximize the margin between linear decision boundary line and 'support vectors'(closest to the linear decision boundary)

In hard margin case, to maximize margin, we solve:

$$
\min_{\mathbf{w}, b} \|\mathbf{w}\|

\text{s.t.} \quad y_i (\mathbf{w} \cdot \mathbf{x}_i - b) \geq 1, \quad \forall i = 1, \dots, N

$$


SVM with kernel




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




