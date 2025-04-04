# How to build chatGPT

reference: https://huyenchip.com/2023/05/02/rlhf.html

![ChatGPT dev steps](./images/1-chatgpt-training.png)

There are three steps to build chatGPT:
- Pretrain LLM.
- Finetune a SFT for dialog.
- RLHF.

## Details of pretraining and finetuning


### During pretraining
- Obviously, data scale is big (TBs), model is big as well (trillions of parameters)
- Sentences are tokenized with subwords(precision between characters and words). (method like: BPE)

```python
  # BPE: Byte Pair Encoding
  "unbelievable runners ran unbelievably fast."
  # ->
  ["un", "believable", " ", "runner", "s", " ", "ran", " ", "unbelievable", "ly", " ", "fast", "."]
    
```
- Next token prediction includes long documents.
- Obviously, training skills are applied:
    - Data augmentation (noise adding, sentences swap)
    - Gradient clipping
    - Weights warm up
- Some calculation tricks are applied:
    - Mix precision

    
### During finetuning
- Data in high-quality and diverse.
- Data includes long conversation.

## RLHF (Reinforcement Learning from Human Feedback)
It is the 3rd step where a Reward Model(RM) is trained and it is used to further finetune the SFT through Proximal Policy Optimization (PPO).

### How to train a RM

After we get a bunch of preference pairs (A, B), meaning A is more preferable over B. 
We can define the loss as following:

$$
L = -\log\left(\frac{\exp(RM(A)) + \exp(RM(B))}{\exp(RM(A))}\right)
$$

Lets write RM as $RM(x, y)$: 

We have a pair $(y_t^{(a)} \| x_t, y_t^{(b)} \| x_t)$, 
- $x_t$ is the current prompt.
- $y_t^{(a)}$ means one response of the model,
- $y_t^{(b)}$ means another response of the model, 
  
and $y_t^{(a)}$ is more preferable than $y_t^{(b)}$.
the loss is:

$$
L = -\log\left(\frac{\exp(RM(x_t, y_t^{(a)})) + \exp(RM(x_t, y_t^{(b)}))}{\exp(RM(x_t, y_t^{(a)}))}\right)
$$

### How to use PPO to finetune the SFT

refer `rl/PPO.md` for the introduction of PPO.

PPO can be regarded as a simple variation of Policy Gradient (PG). In PG, we need know current reward of the state $r_t$ after $a_t$,
and policy function $\pi_{\theta}(a_t \| s_t)$, they are replaced by RM and Language model:

| In PG | In ChatGPT |
|----------|----------|
| $r_t$  | $RM(s_t, a_t)$  |
| $\pi_{\theta}(a_t \| s_t)$ | $\prod_{i=1}^n P_\theta(w_i \mid w_{<i}, s_t)$ |

Note that, the $V_{\phi}(s)$ is finetuned from the SFT drived from previous steps.

