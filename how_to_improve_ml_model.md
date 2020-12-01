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