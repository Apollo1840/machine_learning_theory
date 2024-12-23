# Policy Gradient

reference: https://chatgpt.com/share/6745e845-f458-8009-a645-4d812e2a88ac

## Key concepts:

def. Episode: a series of (state, action, reward).

def. Policy: $𝜋_𝜃(a \mid s)$, which is the probability of taking action $a$ in state $s$, parameterized by $𝜃$ (weights of a neural network, for instance).


## Objective:

The goal is to maximize the **expected cumulative reward** $J(𝜃)$, defined as:


$$
J(\theta) = \mathbb{E}\_{\pi\_\theta} \[ \sum_{t=0}^\infty \gamma^t r_t \]
$$

$$
\sum_{t=0}^\infty \gamma^t r_t = r_0 + \gamma^1 r_1 + \gamma^2 r_2 + ... 
$$

- $r_t$: reward at time step $t$.
- $\gamma$: discount factor.


## Update Rule:

Based on Policy Gradient Theorem, the gradient of $J(𝜃)$ with respect to $𝜃$ is:


$$
\nabla_{𝜃} J(𝜃) = \mathbb{E}\_{\pi\_{𝜃}} \[ \nabla_{𝜃} \log \pi_{𝜃}(a \mid s) \cdot G_t \]
$$


$$
G_t = \sum_{i=t}^\infty \gamma^i r_i = r_t + \gamma^{t+1} r_{t+1} + \gamma^{t+2} r_{t+2} + ... 
$$

- $G_t$: the cumulative reward (return) from time $t$.

Parameters are updated using gradient ascent:

$$
𝜃 \gets 𝜃 + \alpha \nabla_{𝜃} J(𝜃)
$$

- $\alpha$: learning rate.

Note: the expected value $\nabla_{𝜃} J(𝜃)$ needs to be estimated. 


## Estimate the gradient:

### 1. REINFORCE Algorithm:

A Monte Carlo method that uses the sampled return $G_t$ to estimate the gradient:

$$
\nabla_{𝜃} J(𝜃) \approx \sum_t \nabla_{𝜃} \log \pi_{𝜃}(a_t \mid s_t) G_t
$$

For each episode, we will record the whole episode and calculate the discounted rewards ($G_t$) for each $t$,
as well as the dependent variable $\pi_{𝜃}(a_t \mid s_t), $a_t$ is the action with highest probability:

$$
 \{ (s_t, a_t, r_t) \} \Rightarrow \{ (\pi_{𝜃}(a_t \mid s_t), G_t) \}
$$

### 2. Actor-Critic Methods:

Combines policy gradients (actor) with value-based methods (critic). The critic estimates a value function (e.g., $V(s)$ ), which reduces the variance of the gradient estimate.

Introduces the advantage function $A(s, a) = Q(s, a) - V(s)$ to improve stability:

$$
\nabla_{𝜃} J(𝜃) \propto \nabla_{𝜃} \log \pi_{𝜃}(a \mid s) A(s, a)
$$

Since

$$
 Q(s_t, a_t) = r_t + \gamma V(s_{t+1})
$$

$$
{\delta}\_t = A(s_t, a_t) = r_t + \gamma V(s_{t+1}) - V(s_{t})
$$

We will only need to find a proper estimate of $V$ as $V_{\phi}$.

Loss of $V_\phi$:

$$
{{\delta}\_{t \| \phi}}^2 = \left( r_t + \gamma V_\phi(s_{t+1}) - V_\phi(s_t) \right)^2
$$

For each episode, we will record the whole episode and calculate the discounted rewards (${\delta}\_t$) for each $t$,
as well as $\pi_{𝜃}(a_t \mid s_t)$:

$$
 \{ (s_t, a_t, r_t) \} \Rightarrow \{ (\pi_{𝜃}(a_t \mid s_t), {\delta}\_t, {{\delta}\_{t \| \phi}}^2 \})
$$

