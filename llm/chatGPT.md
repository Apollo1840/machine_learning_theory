# How to build chatGPT

reference: https://huyenchip.com/2023/05/02/rlhf.html

![ChatGPT dev steps](./images/1-chatgpt-training.png)

There are three steps to build chatGPT:
- Pretrain LLM.
- Finetune a SFT for dialog.
- RLHF.

## Details of pretraining and finetuning

## RLHF (Reinforcement Learning from Human Feedback)
It is the 3rd step where a Reward Model(RM) is trained and it is used to further finetune the SFT through Proximal Policy Optimization (PPO).

### How to train a RM
### How to use PPO to finetune the SFT

refer `rl/PPO.md` for the introduction of PPO.

PPO can be regarded as a simple variation of Policy Gradient (PG). In PG, we need know current reward of the state $r_t$ after $a_t$,
and policy function $\pi_{\theta}(a_t \| s_t)$, they are replaced by RM and Language model:

| In PG | In ChatGPT |
|----------|----------|
| $r_t$  | $RM(s_t, a_t)$  |
| $\pi_{\theta}(a_t \| s_t)$ | $\prod_{i=1}^n P_\theta(w_i \mid w_{<i}, s_t)$ |


