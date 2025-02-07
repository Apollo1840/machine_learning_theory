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

## High dimensional PE
- Fourier PE 

$$
\gamma(x) = \[ \sin(2\pi Bx), \cos(2\pi Bx) \]
$$

with a high-dimensional random $B$.

## Attention-influcial PE
Introduce biases when calculate attention scores.
Usually incorporate relative distances explicitly.


- Linear Biased PE(LBPE): add a linear bias to the attention score based on relative distance (used in ALiBi/T5).
  
$$
\text{Attention}(Q, K) = \frac{QK^\top}{\sqrt{d}} + b
$$

where $b$ is a learned linear bias term:

$$
b_{i,j} = -m \cdot |i - j|
$$

- Position Biased PE(PBPE): add a correction matrix to the K to encode relative distance information (used in Transformer-XL).

$$
\text{Attention}(Q, K, V) = \text{softmax} \left( \frac{Q K^\top + Q R^\top + u K^\top + v R^\top}{\sqrt{d}} \right) V
$$

- Rotary Positional Embedding(RoPE): Rotate the Q and K based on relative distance.

$$
\mathbf{h}_{\text{rot}}(q, k) = q^\top R^{pos} k
$$

with

$$
\theta_i = 10000^{-2(i-1)/d}
$$