# Neural Architecture Search

## Category
- CNN NAS
- RNN NAS
- Transformer/ViT NAS
- LLM/GPT NAS
- Meta NAS
  - LEMON(https://arxiv.org/abs/2408.16168)


## Methodology

### NAS by EA

#### References:
- Review: https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9504890
- EIC: https://arxiv.org/pdf/1703.01041
- NEAT: https://nn.cs.utexas.edu/downloads/papers/stanley.ec02.pdf
- HyperNEAT: https://www.researchgate.net/publication/23986881_A_Hypercube-Based_Encoding_for_Evolving_Large-Scale_Neural_Networks
- DeepHyperNEAT: 
- HyperNEAT ++: 
- Growth-based Evolutionary Neural Architecture Search:
- Evolutionary Neural Architecture Search with Generative Pre-Trained Model:

#### Introduction
Also called EvoNAS. Focusing on apply Evolution algorithms to search for best Neural network architecture.

**Large-Scale Evolution of Image Classifiers**: 

With complete design of gene, cross-over and mutation.
Focus on the mutation to search for optimal architecture. 


### NAS by RL

#### References
- RL-NAS: https://arxiv.org/pdf/1611.01578
- MnasNet: Platform-Aware Neural Architecture Search for Mobile
- EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks

#### Introduction

**Neural Architecture Search with Reinforcement Learning**:

Use performance on validation set as rewards, and can search for LSTM cell as well.

### NAS by EA+RL
ES(Evolution Strategies) = EA + RL

### Differentiable NAS

**DARTS**: Differentiable Architecture Search 

- EfficientNet, combined with joint strategy.


### One-shot NAS
Search best architecture in a SuperNet.


**Efficient Neural Architecture Search via Parameter Sharing**