# How to improve the performance of the Machine learning model
一个基本的思路还是观察三类表现和训练曲线，判断模型问题，比如是否过拟合，是否弱拟合，然后针对性的进行优化。

但是除此之外，还有一些基本的提升方法，比如数据方面的，和模型集合等可以尝试。

## Improve with Data
总结：创建数据，清洗数据 和 重新抽样（如果必要）。

- First of all, **Increase the data (label) quality** and **get more data** are always the first options but they are always hard to achieve.
- Invent more data with data augmentation.
- (might not good) Invent more data by filling up missing features with statistic assumption. 
- Clean the data with outlier removal.
- Clean the raw data in technical way. (for example, when your raw data is signal).
- (might not good) Sample the marjority to relief label imbalance.

## Improve with Feature engineering
总结：增加或优化特征, 对多个特征进行选择或非线性变换。

Single feature: 

- Rescale the data with normalization.
- Transform the data, for example, use square root inverse to decrease the skewness of the data. 
- Create more feature with domain knowledge. (this requires data collection, might not be possible in real case).
- Create more features based on existed feature. for example, split the string feature, use weekday out of date feature, extract features from signal.

Multiple features:

- Project the data. for example, PCA and some other dimension reduction method.
- Feature selection.

## Improve with split

60/20/20 or 98/1/1

leverage point

k-fold cross validation


## Improve with model
总结：更好的单个模型，或者建设模型群。

- Compare different model.
- Hyperparameter tunning.
- Model ensembling: bagging, boosting, stacking.


## Improve with Training schema
总结：让训练流程更简单，或更科（玄）学。

- Use bootstraping to balance the data.
- Narrow the target or reframe the problem.
- Combine pre-trained model with your model.
- Combine unsurpervised and supervised model.

## Data amount

### Rule of thumb
- More complex models (e.g., large deep neural networks) usually need more data to generalize well.
- Simpler models (e.g., linear regression with few parameters) can often achieve good performance with less data.

What to look at:

- Number of parameters: A neural network with millions (or billions) of parameters generally requires a large dataset—often in the thousands or millions of examples—to avoid severe overfitting.
- Model capacity: Some architectures incorporate regularization (dropout, weight decay, etc.) that can mitigate overfitting, potentially allowing them to do more with less data.
- Task difficulty: Tasks like image classification on complex datasets (e.g., ImageNet) inherently require more data than simpler tasks (e.g., MNIST digit classification).

### Pratical rough guidelines
Below are rough guidelines—these are not hard rules, but starting points:

- Simple tasks (low complexity, few classes) 1,000–10,000 samples can be sufficient, depending on labeling quality and feature complexity.
- Moderately complex tasks (e.g., multiple classes, diverse data) 10,000–100,000 samples may be needed for consistent performance, especially in deep learning contexts.
- High complexity tasks (e.g., large-scale image classification, natural language understanding) 100,000+ (often millions) of examples for modern deep learning methods to work well.


### Practical research
- Reference similar benchmarks.

- Start Small: Collect or label a small dataset to do rapid prototyping. Train a baseline model to see if the problem is tractable.
- Generate a Learning Curve: Add more data in increments, measure how performance improves, and monitor if you approach a plateau.
- Compare Gains vs. Cost: Adding more data means higher labeling costs, collection times, etc. Decide if the performance gains are worth the extra cost.
- Iterate: If the model still shows high variance (overfitting), consider adding more data or applying stronger regularization. If it shows high bias (underfitting), consider a more complex model or more features.

## Model selection
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.one%7C33be4c71-c6b8-4a35-b8fc-8a4f3ae05797%2F%E6%97%A0%E6%A0%87%E9%A2%98%E9%A1%B5%7Cbf090600-823a-4368-888c-98ce7c370208%2F%29&wdorigin=NavigationUrl