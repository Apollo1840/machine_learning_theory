# Basic Machine Learning

References: 
- (My onenote) https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target(ML.one%7Ce8b3e705-493c-431b-b04e-8e9e3752864d%2F04-linear%20regression%7Ccc20eaf9-d27f-4c5e-9886-f21dc3e987f8%2F)&wdorigin=NavigationUrl
- (My onenote) https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2FLinear%20regression%7Cd1449063-187d-41a7-93d4-c0f541144360%2F%29&wdorigin=NavigationUrl

## Categories
Basically, there are three categories of machine learning.
- Supervised learning
- Unsupervised learning
- Semi-supervised learning


### Supervised learning
Training a model with **labeled** data. The model learns to **map** inputs to outputs by minimizing the error between its predictions and the actual labels.

Under supervised learning, there are:
- regression
- classification ...

#### Regression
predicting a **continuous** quantity.

#### Classification
predicting a **discrete** class label - categorical data.



### Unsupervised learning
Deals with **unlabeled** data, with the main goal of finding the **inherent structure** of data.

Under Unsupervised learning, there are 
- clustering ...

### Semi-supervised learning
Uses both labeled and unlabeled data. 
It aims at improving supervised learning performance by **leveraging** a larger amount of unlabeled data, 
typically by helping it learn the underlying structure and **distribution** of data effectively.




## Data
Evolves **Data engineering** and **feature selection**.

Prerequisites of ML, introduced in `data_engineering_for_ml.md` 
and `feature selection.md`. 

## Model
models for:
- supervised learning(`supervised_learning.md`)
- unsupervised learning(`unsupervised_learning.md`)
- semi-supervised learning(`sem_supervised_learning.md`)

### Model hyperparameter tunning
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2F%E4%BB%80%E4%B9%88%E6%98%AFvalidation%7Cbb5bcda5-fc9c-41a4-b7ec-0fe57818b2d5%2F%29&wdorigin=NavigationUrl

Based on validation.

Validation provides an unbiased evaluation of a model. 
except hyperparameter tunning, it can also be used to:
- detect overfitting
- select a model architecture

Cross-validation involves partitioning the data into multiple subsets and using these subsets for both training and validation in different **combinations**. 
It enables effect use of data to get a stronger benefit from utilizing valid datasets.
- leave-one-out
- K-fold


### Model regularization
### Model essembling
see `model_ensembling.md`.

## Metrics

### Bias and Variance 
Two key sources of error in machine learning models.

- Bias: (Too **Stupid**) High bias means the model misses relevant relations, 
  leading to **underfiting**. This often happens to overly simplistic models, resulting in poor performance even on training datasets.
- Variance: (Too **Sensitive**) High variance indicates that the model is too sensitive to small fluctuations, captured noise, and outliers during training, 
  leading to **overfitting**. This often happens when the model has overly high capacity, and has excellent performance on training data but poor generalization to new data.

**Solution**: 
It is hard to reduce bias and variance simultaneously. 
The **trade-off** is managed by:
- choosing the proper model **type** and suitable model **capacity**.
- using **regularization** methods like data augmentation, penalty methods, and model ensembling.

### Measurement
To evaluate the models: `metrics.md`.

# Appendix: Q & A
Knowledges formated as Questions and Answers:
goto: https://github.com/Apollo1840/leetAI
clone it and start it with :

```bash
docker-compose up
```

# Appendix: Industrial
see `industrial_guidance.md`.

# Appendix: Implementation
- Popular Github: https://github.com/eriklindernoren/ML-From-Scratch/blob/master/mlfromscratch
- My Github:  https://github.com/Apollo1840/Machine-Learning-Tech