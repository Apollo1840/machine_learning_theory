# Positional Encoding

## Sinusoidal PE

Principles(advantage) of Sinusoidal PE:
- infinite
- unique
- smooth
- capture short and long range **relativeness** implicityly with periodicity and different wave length.

## Learnable PE

Add to the input before transformer.
- Random PE (fixed-length)
- Learnable PE (fixed-length, BERT-style)
- Dynamic PE (learnable through function, so it is unlimited)

## High dimensional PE
- Fourier PE 

$$
\gamma(x) = [ \sin(2\pi Bx), \cos(2\pi Bx) ]
$$

with a high-dimensional random $B$.

## Attention-influcial PE
Very different from tradictional PE approach, it introduces biases when calculate attention scores.

Usually incorporate relative distances explicitly.


### Linear Biased PE (LBPE): 
Add a linear bias to the **attention score** based on relative distance (used in ALiBi/T5).
  
$$
\text{Attention}(Q, K) = \frac{QK^\top}{\sqrt{d}} + b
$$

where $b$ is a learned linear bias term:

$$
b_{i,j} = -m \cdot |i - j|
$$

### Position Biased PE (PBPE): 
Add a correction matrix to the **K** to encode relative distance information (used in Transformer-XL).

$$
\text{Attention}(Q, K, V) = \text{softmax} \left( \frac{Q K^\top + Q R^\top + u K^\top + v R^\top}{\sqrt{d}} \right) V
$$

$R$ (Relative Encoding Matrix) is a matrix where each row corresponds to a possible relative distance. 

´´´python

Attention score for (i=5, j=3) = Q[5] • K[3] + Q[5] • R[+2]
Attention score for (i=5, j=4) = Q[5] • K[4] + Q[5] • R[+1]  
Attention score for (i=5, j=5) = Q[5] • K[5] + Q[5] • R[0]
Attention score for (i=5, j=6) = Q[5] • K[6] + Q[5] • R[-1]
Attention score for (i=5, j=7) = Q[5] • K[7] + Q[5] • R[-2]

´´´


### Rotary Positional Embedding (RoPE): 
Rotate the Q and K based on relative distance.

$$
\mathbf{h}_{\text{rot}}(q, k) = q^\top R^{pos} k
$$

with

$$
\theta_i = 10000^{-2(i-1)/d}
$$

where $i$ is the distance.

This is equivalent to rotate $q$ a little bit and rotate $k$ a little bit and then do inner product. 

Ps. a matrix $R$ is rotation matrix iff $R^{-1} = R^{\top} \wedge \det(R) = 1$