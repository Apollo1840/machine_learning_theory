
# Feature Selection
references: 
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2F%E7%89%B9%E5%BE%81%E5%B7%A5%E7%A8%8B%7C4b4b192e-ecf1-418e-b6d3-79c5449e9103%2F%29&wdorigin=NavigationUrl

## Why feature selection

- Avoids Curse of Dimensionality (Fail to learn & Distance-failed)
- Prevents overfitting
- Lower computation cost
- Improve interpretablity


## How feature selection

Above all, AIC and BIC are two methods used to balance #features and performance.
We will prefer model with lower AIC or BIC value.

Comparison:
BIC has stronger penalty on complexity of the model.

Strategy:
- If you want a balance between fit and complexity → Use AIC
- If you have a large dataset and want a simpler model → Use BIC

### Statistic-based


- Correlation based (**N**umerical vs **N**umerical)
- T-test to ANOVA (**N**numerical vs **C**ategorical)
- Chi-Square test (**C**ategorical vs **C**ategorical)
- Mutual information (**C**ategorical vs **C**ategorical)


### Correlation based
Drawback: can capture linear relation only.

#### t-test to ANOVA
ANOVA has the same purpose as t-test, but designed for more than two factors and methodolgically based on f-test.

(Ps. f-test can be understood as variance ratio test)

#### Chi-Square test
categorical vs categorical:
1. draw a crosstab
2. calculate expectation table (assume non-relation)
3. use chi-square test

(Ps. chi-square test is used to test whether the variance is significant)

#### Mutual information

$$
\[
I(X; Y) = \sum_{x \in X} \sum_{y \in Y} P(x, y) \log \left( \frac{P(x, y)}{P(x) P(y)} \right)
\]
$$

### Model-based

#### Tree model

#### Neural Net

