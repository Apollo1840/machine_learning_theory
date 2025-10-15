# Model efficiency

## Model structual optimization
NAS with combined target. for NAS, see `NAS.md` for details.

## Model compression
- Prune & L1 regularization
- Low-Rank decomposition
- Parameter sharing & weights clustering

## Calculation optimization
- Mixed Precision & Quantization
  
**Mixed Precision**: In training, we keep FP32 weights in memory, when calculate gradient and updates we use FP16. After the update, we store FP32 checkpoints for next train step (batch). 

**Quantization**: We use FP16 or even FP8 model in inference. 



## Focus on Transformer
- Efficient Transformer variants: 
  https://www.notion.so/Transformer-variants-1605e815919080acb611faed9de730fa?pvs=4
