# Positional Encoding

## Traditional PE

Add to the input before transformer.
- Random PE (fixed-length)
- Learnable PE (fixed-length, BERT-style)
- Sinusoidal PE
- Dynamic PE (learnable, but unlimited)

Principles(advantage) of Sinusoidal PE:
- infinite/unique/smooth
- capture short and long range relativeness implicityly with periodicity and different wave length.


## Attention-influcial PE
Introduce biases when calculate attention scores.


- Linear Biased PE(LBPE): add a linear bias to the attention score based on relative distance (used in ALiBi/T5).
  
$$
\text{Attention}(Q, K) = \frac{QK^\top}{\sqrt{d}} + b
$$

where $b$ is a learned linear bias term:

$$
b_{i,j} = -m \cdot |i - j|
$$

- Rotary Positional Embedding(RoPE): Rotate the Q and K based on relative distance.

$$
\mathbf{h}_{\text{rot}}(q, k) = q^\top R^{pos} k
$$

with

$$
\theta_i = 10000^{-2(i-1)/d}
$$