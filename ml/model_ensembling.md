# Model Ensembling
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2FModel%20ensembles%7C99d21978-2a52-40c3-b291-e74ea0e2b50a%2F%29&wdorigin=NavigationUrl

- Bagging: separate models are trained on multiple subsets of the original datasets(i.e. bootstrapping).
- Boosting: Models are trained one by one, and each new model is trained to correct the errors of the previous models(eg. via weighting).
- Stacking: The prediction of the base learners are input features of the meta-model.

Except for the Stacking method, the final prediction of the model ensemble is the aggregated decision of all those models by hard or soft voting.

Strategy: 
- Bagging: when overfitting.
- Boosting: when only weak models are allowed.
- Stacking: when different strengths of multiple models are needed.
