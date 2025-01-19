# Data Engineering for ML (DEML)

## Avoid selection bias
**Selection bias** occurs when the data collected for a dataset is not representative of the population it's intended to reflect. 
This bias can happen due to **non-random** sampling (eg. systematic exclusion of certain groups).
It can significantly harm the **generalizability** of machine learning models.

How to avoid:
- use-case study
- ensure random selection instead of ranked selection based on availability.
- Differentiating sources of data. Good stratify.



## Data preprocessing

Data filtering:
- Invalid/Missing value removal
- Duplicates removal
- Outlier/Artifacts removal


Data normalizing:
- feature substitution (Integrity normalization)
- Normalization (Numerical normalization): 
    - Standardization
    - min-max normalization
- Transformation (Format normalization)


## Data Augmentation
## Handle Imbalance
Data imbalance occurs when some class in a dataset **significantly outnumbers** some other class.

It often leads to poor performance for the minority class.

Methods:
- (data) Undersampling the majority & Oversampling the minority.
- (data) synthetic minor cases (SMOTE, GAN)
- (model loss) introducing class weights.
- (model loss) focal loss for NN. (in extrem imbalance case)


--

Note: Tree-base models are less sensitive to data imbalance.

