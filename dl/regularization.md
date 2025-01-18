# Regularization

Reference: 
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0.one%7C4ab3a169-69c4-42b8-b4ff-6611a9ee8a28%2F%E6%A8%A1%E5%9E%8B%E6%AD%A3%E5%88%99%E5%8C%96%7Ca138db2e-df10-495a-b840-ceb38ea5af64%2F%29&wdorigin=NavigationUrl

Clues:
- Prevent overfitting directly (DataAug, EarlyStopping)
- Normalize data/weights (batchNorm, LayerNorm)
- Add regularization term (penalty term to loss, such as L1, L2)
- Decrease model capacity (dropout, distillation)
- Adapt model Ensembling


## Data Augmentation
- Noise
- Adversarial

## Model Normalization

- **BatchNorm**: Every feature is normalized independently across a batch.
- **LayerNorm**: Every feature of a single layer with a single input is normalized across each other.
- **InstanceNorm**: (Similar to LayerNorm) Every feature of a single layer with a single input is normalized across each other within one channel.
- **GroupNorm**: Grouped instanceNorm, ie. some channels are grouped.

(P.S. In the inferencing stage of a BatchNorm, the moving average during training is used, instead of the inferencing batch)

- Dropout


## Penalty
- L1
- L2
- l1 & L2 (Elastic)

## Ensemble methods
- bagging
- boosting
- stacking

