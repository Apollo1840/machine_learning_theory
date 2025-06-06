
# Feature Selection
references: 
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2F%E7%89%B9%E5%BE%81%E5%B7%A5%E7%A8%8B%7C4b4b192e-ecf1-418e-b6d3-79c5449e9103%2F%29&wdorigin=NavigationUrl

Feature selection is selecting a subset of relevant features (variables, predictors) for use in model construction.

## Why feature selection

- Lower (computation: training/working) cost
- Reduce overfitting
- Emplifies model hence improve interpretablity
- Avoids Curse of Dimensionality(CoD) (Fail to learn & Distance-failed)


## How feature selection

Strategy: 
- If you have a large number of features (e.g., high-dimensional data) → Filter methods (e.g., Mutual Information, PCA)
- If computational cost is not a concern and you need high accuracy → Wrapper methods (e.g., RFE, SeqFS)
- If using tree-based models → Embedded methods (e.g., Feature importance from Random Forest, XGBoost)
- If using deep learning models → SHAP


Above all, **AIC** and **BIC** are two methods used to balance #features and performance.
We will prefer model with lower AIC or BIC value.

Comparison:
BIC has stronger penalty on complexity of the model.

Strategy:
- If you want a balance between fit and complexity → Use AIC
- If you have a large dataset and want a simpler model → Use BIC

### Filter methods (Statistics-based)

-  **N**umerical vs **N**umerical (N vs N): Correlation based
- **N**umerical vs **C**ategorical (N vs C): t-test, ANOVA
- **C**ategorical vs **C**ategorical(C vs C): Chi-Square test, Mutual information 

#### N -> N

**Correlation based**:

Drawback: can capture linear relation only.

#### N -> C

**t-test to f-test**:

ANOVA has the same purpose as t-test, but designed for more than two factors and methodolgically based on f-test.

(Ps. f-test can be understood as variance ratio test; ANOVA is a method that uses the F-test to compare the means of multiple groups)

#### C -> C

**Chi-Square test**:

1. draw a crosstab
2. calculate expectation table (assume non-relation)
3. use chi-square test

(Ps. chi-square test is used to test whether the variance is significant)

For numerical feature: discretization via creating bins.

**Mutual information(MI)**:

MI measures the reduction in uncertainty about Y given knowledge of X.
Or amount of shared information between X and Y.

MI = KL(P(x,y)||P(x)P(y)):

$$
I(X; Y) = \sum_{x \in X} \sum_{y \in Y} P(x, y) \log \left( \frac{P(x, y)}{P(x) P(y)} \right)
$$

(memorize tip: $\frac{P(x, y)}{P(x) P(y)}$ often used to measure dependency).

For numerical feature: 
- discretization via creating bins.
- (more common) use k-th NN to estimate the entropy and measure MI by entropy of X, Y and (X, Y).
Since $I(x; Y)=H(x)+H(y)-H(x, y)$.

Comments:

- Advantage of MI as FS:
  - Both numerical and categorical features.
  - Capture non-linear relationship and has no assumption of the distribution.
  - (variant mRMR is robust to feature redundance).
- Dissadvantage of MI as FS:
  - Since it  has no assumption of the distribution, it is prune to
    - noisy random dependency
    - high cardinality feature, because more likely to have noisy dependency

### Wrapper methods (Model-based)

- Random feature elimination (RFE) (needs importance measure)
- Sequential feature selection (SeqFS)
  - SFS-Backwards 
  - SFS-Forwards
  - BiFS
- GA
- Lasso regression(L1)


Feature importance:
- Coefficients in linear alike model. (such as linear regression, SVM)
- Mean Decrease in Accuracy (**MDA**): After randomly shuffled THE feature of inputs.
- Mean Decrease in Impurity (**MDI**): Decrease of Gini score in DT.

(P.S wrapper methods are robust to redundant features)

#### in Random forest

DT: Impurity decrease is **weighted** by number of points in each decision node.

RF: Importance is **sumed** upon all decision trees. 

#### in Neural Net

SHAP: 
SHAP value measures how feature contributes to certain output (by removing that feature). 
Average absolut SHAP value measures the importance of features.

reference: https://arxiv.org/abs/1705.07874v2

### Dimension reduction
- PCA, LDA
- t-SNE, UMAP