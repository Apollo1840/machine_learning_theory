# Monte-Carlo & TD methods

## Estimate V(s)

### Monte Carlo (MC) Target (Rewards-to-go)

The critic is trained by minimizing the mean squared error (MSE) between its output and the full return (rewards-to-go). For a state $s_t$, the loss is

$$
L_{\text{MC}}(\phi) = \frac{1}{2} \left( V_\phi(s_t) - R_t \right)^2,
$$

where Rewards-to-go is: 

$$
R_t = r_t + \gamma r_{t+1} + \gamma^2 r_{t+2} + \cdots.
$$

This target is an **unbiased** estimator of the true value $V_\pi(s_t)$ but often has high variance, especially in long or stochastic episodes.

#### Temporal Difference (TD) Target (One-step Bootstrapping)

Here the critic is trained by minimizing the squared TD error:

$$
L_{\text{TD}}(\phi) = \frac{1}{2} \left( V_\phi(s_t) - TD_t \right)^2.
$$

where TD(0) target is:

$$
TD_t = r_{t+1} + \gamma V_\phi(s_{t+1}) 
$$

Although this target is **biased** (since it depends on the current estimate $V_\phi(s_{t+1})$ ), 
it generally has lower variance than the full-return target.

In many practical AC algorithms (especially on-policy methods), TD methods (TD(0)) are preferred
because the reduction in variance and improved sample efficiency tend to outweigh the bias introduced by bootstrapping.

