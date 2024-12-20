# CLIP
reference: 
- Intro: https://openai.com/index/clip/
- Paper: https://arxiv.org/pdf/2103.00020

## Prerequisites

### InfoNCE loss
Sysmetric loss combined from `L_image(L1)` and `L_text(L2)`, where the terms measure how good the model find a correct pair for each instance. 
![infoNCE Loss](https://github.com/Apollo1840/machine_learning_theory/blob/main/multi-modal/images/infoNCE.jpg?raw=true)

## Procedure
1. Dataset Creation
 -  Data: Collect a large-scale dataset of (image, text) pairs from the internet. The authors used 400 million such pairs for CLIP's training.
 - Preprocessing: Normalize images and tokenize texts using preprocessing methods suitable for the model (e.g., resizing images, applying text tokenization like Byte Pair Encoding).
2. Model Architecture
 - Image Encoder: Use models such as ResNet or Vision Transformer to encode images into fixed-dimensional embeddings.
 - Text Encoder: Use a Transformer-based text encoder to convert tokenized text into fixed-dimensional embeddings.
3. Training Objective
 - Minimise InfoNCE Loss to maximize the cosine similarity of correct pairs.
4. Training Details
 -  Batching: Use large batches (e.g., 32,768 pairs) to increase diversity and stabilization in training.
5. Evaluation
After training, evaluate the model's zero-shot transfer capability by generating text prompts corresponding to target tasks (e.g., class names) and computing similarity scores with images.
Test on various datasets to measure generalization and task adaptability.
