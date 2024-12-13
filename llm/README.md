# Large Language Models

## Theory

| Model     | Type      |  Encoder | Decoder
|---------------|---------------|-------------|-------------|
| Native Transformer; T5 | Encoder-Decoder | x | x|
| GPT | Decoder-Only |  | x|
| BERT | Encoder-Only |x | |

### BERT (Bidirectional Encoder Representations from Transformers)
reference: https://arxiv.org/pdf/1810.04805

Based on **Token trick**. Use MLM and NSP to pretrain the model.

```bash

# Masked Language Modeling (MLM)
# Input: A sentence with some tokens masked.
Input:  "The quick [MASK] fox jumps over the lazy dog."
Output: "The quick brown  fox jumps over the lazy dog."

# Next Sentence Prediction (NSP)
# Input: Two sentences with a label indicating whether the second sentence follows the first.
Input:  "[CLS]  The sky is blue. [SEP] It is a beautiful day. [SEP]"
Output: "IsNext The sky is blue. [SEP] It is a beautiful day. [SEP]"  

```

### GPT (Generative Pre-trained Transformer)
reference: https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf


Based on **NLG trick**. Use text generation to pretrain the model and use text generation to reform other NLP tasks.

```bash

# Classifier reform
"The movie was fantastic!" => "Positive" 
# Reform to :
Input:  "The movie was fantastic! Sentiment: "
Output: "movie was fantastic! Sentiment: Positive"

```



## Implementation

### Chatbot

How is ChatGPT built: `how_to_build_chatGPT.md`.

### Prompt engineering

### RAG
refer to `RAG.md`.

### Reasoning AI

