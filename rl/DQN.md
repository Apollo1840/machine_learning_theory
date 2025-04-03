# Deep Q-Networks (DQN)
What It Does: Uses a neural network to approximate the Q-value function `Q(s,a)`, mapping state-action pairs to their expected cumulative rewards.
How It Works:
The agent collects experience tuples `(s,a,r,s′)` and stores them in a replay buffer.
The neural network learns to minimize the Temporal Difference (TD) error:

$$
\text{Loss} = \[ r + \gamma \max_{a'} Q_{\xi}(s', a') - Q_{\theta}(s, a) \]^2
$$
 
where target $Q_{\xi}$ is a separate target network updated periodically.

Advantages:
- Can handle very large or continuous state spaces.
- Learns efficiently using replay buffers and target networks.


## Update of target network

In online DQN, there is a FIFO replay buffer, training batch is sampled from this buffer.
This is buffer is updating based on current policy at each environment step and after a fixed number of enviroment steps,
the target network will be updated. 


In offline DQN, target network updated after several training steps or episodes.