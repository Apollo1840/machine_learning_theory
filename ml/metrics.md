# Metrics


## Metrics for regression
reference:  https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2FMetrics%20%E5%A6%82%E4%BD%95%E8%AF%84%E4%BC%B0%E5%9B%9E%E5%BD%92%E5%99%A8%7Ca08eb10f-50ab-4f16-8ac6-922d636fbb49%2F%29&wdorigin=NavigationUrl

### $R^2$
The R-squared value measures the fitness of a regression model.

It represents how much of the percentage of the variance of a dependent variable can be **explained** by the model.

(Interestingly, if the model is the linear regression of one dependent variable, R square is equal to the squared correlation value (R))

## Metrics for classification

### Confusion matrix
A confusion matrix is used to indicate the performance of a classifier. It is typically formatted as a four-element matrix. Denote number of instances which are actual positive or negative, predicted as positive or negative.

- Type I Error: accepted negative, i.e false alarm
- Type II Error: rejected positive, i.e miss

| TP | FP | TN | FN |
| ---- | ---- | ---- | ---- | 

- accuracy: T/A
- precision (ppr): TP/pP
- recall (sensitivity/sen, TP rate): TP/rP
- reverse recall (specificity/spe, 1-FP rate): TN/rN

(PS: ** rate: based on real condition)

Curves:
- PR curve: Precision to Recall.
- ROC curve: `1 - recall_reverse` to `recall` (= 1-spe to sen)(= FP rate to TP rate)

ROC curve explaination: 
- bottom left means high Error II rate, all missed.
- upper right means high Error I rate, all false alarmed.

Metric:
- AUC: area under ROC curve. 
- F1score: decimal average of precision and recall.
- F-beta score: emphasis on recall if beta>1.

Explain with examples: 
https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2FMetrics%20%E5%A6%82%E4%BD%95%E8%AF%84%E4%BC%B0%E5%88%86%E7%B1%BB%E5%99%A8%7C39c96090-bc5a-4f4e-aa51-1ab3d1feaa92%2F%29&wdorigin=NavigationUrl


### Micro- and Macro-
For performance measure of multi-class classification.
- Macro-average: average F1.
- Micro-average: harmonic average of weighted precision and recall, roughly weighted average F1.(NOT equal!)


## Metrics for clustering

reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2FMetrics%20%E5%A6%82%E4%BD%95%E8%AF%84%E4%BC%B0%E8%81%9A%E7%B1%BB%E5%99%A8%7Ca3e931fe-6a1c-4b89-9049-24eb37da0b14%2F%29&wdorigin=NavigationUrl

- (point) Silhouette Score: measures how well each point lies within its cluster.
- (max) DB Index : measures the average most different cluster discrepancy ratio for each cluster.
- (tr) Variance Ratio Criterion: measures the ratio of between-cluster to within-cluster variance.

tips:
- Silhouette Score ask each **people** how well they like fit into group.
- DB index ask **leader** of the each how well they feel totally different from one other group.
- VRC ask the **organizer** how different the groups are compare to how cohesive within group is.