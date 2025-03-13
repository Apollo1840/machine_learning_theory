# Prerequisites

## Curse of Dimensionality
- Distance fail: ratio of nearest to farest converge to 1.
- Local structure fail: too sparse, points hard to fill up the space; sphere hard to fill the hyper-cube.
- Overfiting

## Entropy of points cloud

We can use k-th NN to estimate the entropy:
1. Use k-th NN to estimate the density
2. use density to calculate the entropy

$$
p(x_i) \approx \frac{k}{N V_d(\epsilon_i)}
$$

$$
H(X) \approx - \frac{1}{N} \sum_{i=1}^{N} \log p(x_i)
$$

(Ps. Alternative: Kernel density estimation)