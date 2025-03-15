# Model uncertainty

## Evident deep learning(EDL)

Two factors:
- Use softplus for evidence prediction.
- Use EDL loss instead of CE loss.

**Evidence prediction**

The model predict logits, linearly use logits to calculate the probability, 
instead of using exponential as softmax.

By this, `S = sum(all logits) + #cls` can be regarded as total amount of evidence, 
and use `#cls/S` to measure the uncertainty of this prediction.

**EDL loss**

Combination of NLL loss and a KL term to normalize evidence distribution.

- Model Uncertainty = `#cls/S`
- Data Uncertainty = `1 - max_i (logit_i + 1)/S`


(P.S a more theroretical justified version of EDL use digamma function to measure classification discrepancy 
and use KL between Pn instead of logit_i + 1 to normalize evidence distribution. Training will be more smooth and stable)