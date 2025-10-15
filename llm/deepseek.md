# How to build Deepseek

Compare to chatGPT.

Deepseek has three major differences:
- Heavier SFT
- GPRO instead of PPO (introduced `rl/PPO.md`)
- Multi-head Latent Attention (MLaA)

## Multi-head Latent Attention(MLaA)

The core idea is to not have every token attend to every other token directly. Instead, all tokens first "summarize" their information by interacting with a fixed set of k latent vectors. Then, the latent vectors aggregate this global information, which the tokens can subsequently attend to.

