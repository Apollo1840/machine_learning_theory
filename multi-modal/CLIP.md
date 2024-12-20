# CLIP

reference: https://arxiv.org/pdf/2103.00020

## Prerequisites

### InfoNCE loss
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
4. Training Procedure
Initialization: Start with random weights for both encoders or optionally use pretrained weights if available.
Batching: Use large batches (e.g., 32,768 pairs) to increase diversity and stabilization in training.
Optimizer: Use Adam with weight decay regularization.
Learning Rate Schedule: Use a cosine annealing learning rate schedule for smooth decay.
Data Augmentation: Apply augmentations to images (e.g., random cropping) to improve generalization.
5. Scaling
Use larger models and compute resources as necessary. CLIP scaled from ResNet-50 to larger models like Vision Transformer (ViT-L/14).
Train for a sufficient number of epochs to ensure convergence, often requiring significant computational resources.
6. Evaluation
After training, evaluate the model's zero-shot transfer capability by generating text prompts corresponding to target tasks (e.g., class names) and computing similarity scores with images.
Test on various datasets to measure generalization and task adaptability.
