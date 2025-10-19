# How to build Deepseek

Compare to chatGPT.

Deepseek has three major differences:
- Heavier SFT
- GPRO instead of PPO (introduced `rl/PPO.md`)
- Multi-head Latent Attention (MLaA)

## Multi-head Latent Attention(MLaA)

The core idea is to not have every token attend to every other token directly. Instead, all tokens first "summarize" their information by interacting with a fixed set of k latent vectors ($Q_L$).

Based on $Q_L$, $K$, $V$ of tokens will get their $K_L$ and $V_L$. Note that size of $K_L$ and $V_L$ are equal to size of $Q_L$, ie, k. 

$Q$ of tokens, which originally responsible to get the attention scores, now interact with $K_L$ to get attentions scores and aggregate $V_L$.

