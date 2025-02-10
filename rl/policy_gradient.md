# Policy Gradient

reference:
- (openAI definition) https://spinningup.openai.com/en/latest/algorithms/vpg.html
- (theory with implementation) https://chatgpt.com/share/6745e845-f458-8009-a645-4d812e2a88ac
- (implementation of Vanilla AC): https://github.com/jihoonerd/actor-critic/tree/main


---

Policy Gradient is a method direct learn the policy function - $𝜋_𝜃(a \mid s)$. 

So it could also be called $\pi$-learning, considering Q-learning is to learn the `Q(s, a)` table. 

It belongs to **on-line, model-free, on-policy** category of RL.

## Prequisities

### $𝜋_𝜃(a \mid s)$ & $\nabla_{𝜃} 𝜋_𝜃(a_t \mid s_t)$

### Policy Representation

The policy \( \pi_\theta(a \mid s) \) is defined as the probability of taking action \( a \) given state \( s \), and it is parameterized by \( \theta \).

### Neural Network Modeling

A common approach is to define a function
\[
f_\theta(s) = \hat{a},
\]
where \( \hat{a} \) is a vector representing a probability distribution over actions. In other words, the neural network parameterized by \( \theta \) outputs a probability distribution from which an action is sampled.



### Action Selection

Given a state \( s_t \), the network produces
\[
\hat{a_t} = f_\theta(s_t),
\]
which is a probability distribution over possible actions. If the action \( a_t \) is represented as a one-hot vector, the probability of selecting \( a_t \) is given by
\[
\pi_\theta(a_t \mid s_t) = a_t^\top \hat{a_t},
\]
resulting in a scalar probability.


### Gradient of the Log-Probability

In policy gradient methods, it is common to work with the gradient of the log-probability:
\[
\nabla_\theta \log \pi_\theta(a_t \mid s_t).
\]
This gradient has the same shape as \( \theta \) and is essential for updating the policy parameters.


### Discrete Example

Consider a simple discrete case where the policy is modeled as:
\[
f_\theta(s_t) = \operatorname{Softmax}(\theta s_t),
\]
with \( \theta \) being an \( M \times N \) matrix (assuming \( M \) actions and \( s_t \in \mathbb{R}^N \)). Here, the output \( \hat{a_t} \) is obtained by applying the softmax function to \( \theta s_t \).

For a one-hot encoded action \( a_t \), the gradient of the log-probability is given by:
\[
\nabla_\theta \log \pi_\theta(a_t \mid s_t) = (a_t - \hat{a_t}) \otimes s_t,
\]
where the outer product \( \otimes \) ensures that for each action \( i \) (i.e., each row of \( \theta \)), the gradient is:
\[
\nabla_{\theta_i} \log \pi_\theta(a_t \mid s_t) = \bigl(a_t(i) - \hat{a_t}(i)\bigr) s_t.
\]


### Continuous Case

In continuous control problems, the policy \( \pi_\theta(a \mid s) \) is often modeled using a probability distribution over continuous actions (for example, a Gaussian distribution). In this case, the neural network outputs the parameters (e.g., mean and variance) of the distribution, and similar gradient computations apply in order to update \( \theta \).

---

$𝜋_𝜃(a \mid s)$ can be understood as $a = f_{\theta}(s)$,
and we can use an neuro network to model $f_{\theta}$.
Give $s_t$, we can calculate $\hat{a_t}$ (a probability distribution), 
that the chosen action $a_t$ is typically sampled from. 

$𝜋_𝜃(a_t \mid s_t)$ is a scalar, representing the probability of choosing $a_t$ responding $s_t$.
So $\nabla_{𝜃} 𝜋_𝜃(a_t \mid s_t)$ is a same shape variable of $\theta$, 

For example, one-hot vector $a_t^{T}$ times probability distribution $\hat{a_t}$.

Lets make a trival discrete example:

$f_{\theta}(s_t) = Softmax(\theta * s_t)$ where $\theta$ is a M*N matrix.

Then the $\nabla_{𝜃} \log 𝜋_𝜃(a_t \mid s_t) =  (a_t - \hat{a_t}) \otimes s_t $, where $a_t$ is the one-hot vector.

In continous (control) example, a probabilitical model is often trained.


## Objective:

The goal is to find proper $\theta$ in $𝜋_𝜃(a \mid s)$ via maximizing the **expected cumulative reward** $J(𝜃)$, defined as:


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
\nabla_{𝜃} J(𝜃) = \mathbb{E}\_{\pi\_{𝜃}, t} \[ \nabla_{𝜃} \log \pi_{𝜃}(a \mid s) \cdot G_t \]
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
.

Since

$$
 Q(s_t, a_t) \approx r_t + \gamma V(s_{t+1})
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

