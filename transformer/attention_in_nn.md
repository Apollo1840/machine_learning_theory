# Attention
Attention mechanisms enable models to **focus** on relevant parts of the input data(or feature map) by calculating a **weighted** sum of input features based on alignment scores(or attention scores).

Those scores are often calculated via the dot product of queries and keys. The query vector can be:
- uniform for all input tokens(Luong Attention), or
- different at each position(Self-attention) and generated from input tokens just like the keys.