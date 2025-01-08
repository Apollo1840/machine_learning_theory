# Metrics


## Metrics for regression
reference:  https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2FMetrics%20%E5%A6%82%E4%BD%95%E8%AF%84%E4%BC%B0%E5%9B%9E%E5%BD%92%E5%99%A8%7Ca08eb10f-50ab-4f16-8ac6-922d636fbb49%2F%29&wdorigin=NavigationUrl


## Metrics for classification
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2FMetrics%20%E5%A6%82%E4%BD%95%E8%AF%84%E4%BC%B0%E5%88%86%E7%B1%BB%E5%99%A8%7C39c96090-bc5a-4f4e-aa51-1ab3d1feaa92%2F%29&wdorigin=NavigationUrl

| TP | FP | TN | FN |
| ---- | ---- | ---- | ---- | 

accuracy: T/A

sensitivity: TP/P

specificity: TN/N

ROC: sensitivity(x) to 1-specificity(y)

Imagine, you have several apples, some are good, some are bad. You ask your child (the model) to pick them: keep the good apples, and throw the bad apples. 

True is the good apples kept and the bad apples thrown.

False is the bad apples kept (Error I) and the good apples thrown (Error II).

Positive is the apples your child keep.

Negative is the apples your child thrown.

Accuracy is the True/All

There are two aspect to evaluate the model: precision and recall.

Precision is easy.

postive precision is the ratio of good apples compare to what your chlid kept.

negative precision is the ratio of of bad apples compare to what your child thrown.

Recall is more interesting.

positve recall (sensitivity) is the ratio of good apples you have compare to all good apples. 

negative recall (specifictiy) is the of ratio of bad apples your child thrown compare to all bad apples. 

## Metrics for clustering

reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2FMetrics%20%E5%A6%82%E4%BD%95%E8%AF%84%E4%BC%B0%E8%81%9A%E7%B1%BB%E5%99%A8%7Ca3e931fe-6a1c-4b89-9049-24eb37da0b14%2F%29&wdorigin=NavigationUrl