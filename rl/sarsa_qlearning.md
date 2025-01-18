# SARSA & Q-learning
They are both online, model-free RL methods.
They both try to update `Q(s, a)` **Table** to get best policy as:
`a|s = argmax(Q(s, a)).`

**Q-Learning**

- Off-policy: Learns the optimal policy independently of the agent's behavior.
- Update rule uses the **maximum future reward**.
- Suitable for deterministic environments and faster convergence.

Update rule:

$$
Q(s, a) \gets Q(s, a) + \alpha \[r + \gamma \max_{a'} Q(s', a') - Q(s, a) \]
$$

**SARSA**

- On-policy: Learns based on the agent's actual actions.
- Update rule depends on the **action taken by the current policy**.
- Better for stochastic environments and safer exploration.

Update rule:

$$
Q(s, a) \gets Q(s, a) + \alpha \[r + \gamma Q(s', a') - Q(s, a) \]
$$

# Outlook
SARSA & Q-Learning requires finite state and action space. 
DQN generalized the Q(s, a) function and then only requires finite action space. see `DQN.md` for details.