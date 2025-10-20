# Llama
- reference: https://cvpr.thecvf.com/virtual/2025/invited-talk/35403

## Shared component

- **RMSNorm (Root Mean Square Normalization)**: Replaces traditional LayerNorm to stabilize the training process and improve efficiency.

- **SwiGLU** Activation Function: Replaces standard ReLU or GeLU to boost model performance.

- **RoPE (Rotary Positional Embeddings)**: Replaces absolute positional encoding, which better handles the relative position relationships of Tokens in a sequence, helping the model understand long sequences.