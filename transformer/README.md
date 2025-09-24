# Transformer

## Intro

- Detailed intro with implementation on pytorch (TrnPPT): https://docs.google.com/presentation/d/1uDqKkrXPaOFeKrQXSwY7KXhvx2aVZ07x3pVVM4OVfH8/edit#slide=id.g31d09b857a6_0_55

### Word embedding
Fully trainable and use transpose as reverse. Key insights: the dot product is a measure of similarity.

### Positional encoding
Introduced in TrnPPT.

see `positional_encoding.md`.

### Scaled dot attention
Introduced in TrnPPT.

key points to repeat:
- why we need scaled with $\sqrt{d_k}$: we do not want the variance of raw attention score to be high. Huge difference makes the gradient of Softmax small. (Ps. this scale is multiply to embedding as well to make the scale aligned)

More about attention see `attention_in_nn.md`.

### Multi-head Attention (MHA)
Introduced in TrnPPT.

key points to repeat:
- Lenght of implicit representation of tokens is not changed. Larger number of head makes the each aspect representation become smaller. 

### Transformer Encoder Block
Introduced in TrnPPT. 

Key points to repeat:
- FN is one layer of neuro, ie. two Linear Projections (with Relu).
- Dropout after MHA and FN
- (Post-LN) Skip connection before LayerNorm. 
  
$x_{l+1} = \mathrm{LN}\!\Big(x_l + \mathrm{SubLayer}(x_l)\Big)$.

Modern transformers prefer Pre-LN, ie.

$x_{l+1} = x_l + \mathrm{SubLayer}\!\big(\mathrm{LN}(x_l)\big)$


### Transformer Decoder Block
Introudced in TrnPPT.

Key points to repeat:
- Decoder block has three sub-module
- The output of first block directly use Queries input (not directly as queries).

## Transformer visualization 
https://github.com/Apollo1840/transformer/blob/main/visual_model_attn.py

- A straightforward heatmap for global overview.
- Detailed line-based plots to understand token-to-token interactions.
- Extended multi-head visualizations to compare contributions across different attention heads, with focusing on certain token, man can observe different aspectives of heads.

## Training a Transformer 

- How to train a Transformer for machine translation: https://docs.google.com/presentation/d/1XLpuKlBQSuXCXQS1cbYu4S7LsuWVqzutIMuD2mAaEsU/edit#slide=id.g31d00a118d9_0_81

## Transformer variants
https://www.notion.so/Transformer-variants-1605e815919080acb611faed9de730fa?pvs=4

### Modern Transformer

Updates:
- Sparse attention window.
- Use relative PE, such as rotation PE.
- PE contributes to each layer.
- ReLU -> SiLU -> SwiGLU(A complex gate system as a replacement for FFN).
- Remove dropout.
- Remove biase in Linear layer.
- use Pre-LN.
- pretrain task: n-gram masking.
- pretrain task: token replacement detection.
