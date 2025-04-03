# Policy Gradient

reference:
- (openAI definition) https://spinningup.openai.com/en/latest/algorithms/vpg.html
- (theory with implementation) https://chatgpt.com/share/6745e845-f458-8009-a645-4d812e2a88ac
- (implementation of Vanilla AC): https://github.com/jihoonerd/actor-critic/tree/main


---

Policy Gradient is a method direct learn the policy function - $𝜋_𝜃(a \mid s)$. 

So it could also be called $\pi$-learning, considering Q-learning is to learn the `Q(s, a)` table. 

It belongs to **on-line, model-free, on-policy** category of RL. And the state space and action space are **infinite**.
## Prequisities

### Policy and Policy gradient ($𝜋_𝜃(a \mid s)$ & $\nabla_{𝜃} \log 𝜋_𝜃(a_t \mid s_t))$

$𝜋_𝜃(a \mid s)$ can be understood as $a = f_{\theta}(s)$,
and we can use an neuro network to model $f_{\theta}$.
Give $s_t$, we can calculate $\hat{a_t}$ (a probability distribution), 
from which the chosen action $a_t$ is typically sampled. 

$𝜋_𝜃(a_t \mid s_t)$ is a scalar (eg. one-hot vector $a_t^{T}$ times probability distribution $\hat{a_t}$.
), representing the probability of choosing $a_t$ responding $s_t$.
So $\nabla_{𝜃} \log 𝜋_𝜃(a_t \mid s_t)$ is a same shape variable of $\theta$, 

#### Examples

First, let's make a trival discrete example:

$f_{\theta}(s_t) = Softmax(\theta * s_t)$ where $\theta$ is a M*N matrix.

Then the $\nabla_{𝜃} \log 𝜋_𝜃(a_t \mid s_t) =  (a_t - \hat{a_t}) \otimes s_t $, where $a_t$ is the one-hot vector.

In continous (control) example, a probabilitical model is often trained.

### General PG process

In PG method, we will modeling the **Policy function**. 

We will run one episode (or a batch of episodes) based on current policy, 
to collect one (or a batch of) **Trajectories**.
From those trajectories, we could calculate the **Gradient** for updating the policy function.

Typically, we end the loop after several rounds.

## Theory

### Objective:

The goal is to find proper $\theta$ in $𝜋_𝜃(a \mid s)$ via maximizing the **expected cumulative reward** $J(𝜃)$, defined as:


$$
J(\theta) = \mathbb{E}\_{\pi\_\theta} \[ \sum_{t=0}^\infty \gamma^t r_t \]
$$

$$
\sum_{t=0}^\infty \gamma^t r_t = r_0 + \gamma^1 r_1 + \gamma^2 r_2 + ... 
$$

- $r_t$: reward at time step $t$.
- $\gamma$: discount factor.

(Note: $J(\theta)$ is espected Rewards-to-go from initial state.)
### Update Rule:

Based on Policy Gradient Theorem, the gradient of $J(𝜃)$ with respect to $𝜃$ is:


$$
\nabla_{𝜃} J(𝜃) = \mathbb{E}\_{\pi\_{𝜃}, t} \[ \nabla_{𝜃} \log \pi_{𝜃}(a \mid s) \cdot G_t \]
$$


$$
G_t = \sum_{i=t}^\infty \gamma^{i-t} r_i = r_t + \gamma r_{t+1} + \gamma^{2} r_{t+2} + ... 
$$

- $G_t$: the cumulative reward (return) from time $t$.

Parameters are updated using gradient ascent:

$$
𝜃 \gets 𝜃 + \alpha \nabla_{𝜃} J(𝜃)
$$

- $\alpha$: learning rate.



### Estimate the gradient:

Note that, the expected value $\nabla_{𝜃} J(𝜃)$ needs to be estimated. 

Different PG methods has their own way to estimate $\nabla_{𝜃} J(𝜃)$, such as:
- (REINFORCE) $\nabla_{𝜃} J(𝜃) \approx \sum_t \nabla_{𝜃} \log \pi_{𝜃}(a_t \mid s_t) G_t$
- (AC) $\nabla_{𝜃} J(𝜃) \propto \nabla_{𝜃} \log \pi_{𝜃}(a \mid s)\[Q(s, a)-v(s)\]$


## Methods

### 1. REINFORCE Algorithm:

A Monte Carlo method that uses the sampled return $G_t$ to estimate the gradient:

$$
\nabla_{𝜃} J(𝜃) \approx \sum_t \nabla_{𝜃} \log \pi_{𝜃}(a_t \mid s_t) G_t
$$

For each episode, we will record the whole episode and calculate the discounted rewards ($G_t$, also called rewards-to-go) for each $t$,
as well as the dependent variable $\pi_{𝜃}(a_t \mid s_t)$, $a_t$ is the action with highest probability:

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
 Q(s_t, a_t) \approx r_t + \gamma V(s_{t+1})
$$

$$
{\delta}\_t := A(s_t, a_t) = r_t + \gamma V(s_{t+1}) - V(s_{t})
$$

We will only need to find a proper estimate of $V$ as $V_{\phi}$.

Here we take TD method(see `mc_td.md` for more details) for estimating V(s) as example, loss of $V_\phi$:

$$
{{\delta}\_{t \| \phi}}^2 = \left( r_t + \gamma V_\phi(s_{t+1}) - V_\phi(s_t) \right)^2
$$

For each episode, we will record the whole episode and calculate the discounted rewards (${\delta}\_t$) for each $t$,
as well as $\pi_{𝜃}(a_t \mid s_t)$:

$$
 \{ (s_t, a_t, r_t) \} \Rightarrow \{ (\pi_{𝜃}(a_t \mid s_t), {\delta}\_t, {{\delta}\_{t \| \phi}}^2 \})
$$

(P.S OpenAI name MC methods for Critic estimate as Vanilla PG (VPG) method, see: https://spinningup.openai.com/en/latest/algorithms/vpg.html).

### 3. GRPO

Same as AC methods, Introduces the advantage function $A(s, a)$:

$$
\nabla_{𝜃} J(𝜃) \propto \nabla_{𝜃} \log \pi_{𝜃}(a \mid s) A(s, a)
$$

However, we do not use $Q(s, a) - V(s)$ to quantify A(s, a), instead we use group relative advantage 
to estimate A(s, a). i.e we adapt several actions simultaneously in a group and based on their different rewards-to-go, based on
calculate the relative advantage as advance score (scaled difference over average). 

And in GRPO, the update limitation trick from PPO method (see `ppo.md`) is also used.
