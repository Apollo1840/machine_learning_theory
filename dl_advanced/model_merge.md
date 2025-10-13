# Model Ensemble


## Trivial Ensemble
Focus on output level, do soft-voting, hard-voting, confidence-based voting of the models.

## Model Merge
Ensemble in a deeper level. It normally means averaging weights of mono-morphic models.

## Mix of experts (MoE)
Features from sub-models of different architecture will get aggregated via attention scores. 

Normally we do hard combination of top-K features instead of soft combination overall (To save computation power). 