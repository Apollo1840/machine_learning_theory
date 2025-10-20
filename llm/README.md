# Large Language Models (LLM)

## Introduction

An area significantly improved performance of solving classic Doc2Doc problem. 
The reason behind it is its true emerged 'intelligence'.
Hence we use it solve modern Doc2Doc Problem (or modern NLP Problem) such as:
- small talk
  - role play
- direct Q&A 
  - common sense, common reasoning
  - clear defined STEM challenges
- creation
  - problem-solving code
  - artworks
- high-level pattern learning
  - input-output pair learning, figure out the pattern
- tool usage
  - use information-processing helper tools
    - to answer question
    - to create
  - interact with simulation tools


## Theory

| Model     | Type      |  Encoder | Decoder
|---------------|---------------|-------------|-------------|
| Native Transformer; T5 | Encoder-Decoder | x | x|
| BERT | Encoder-Only |x | |
| GPT | Decoder-Only |  | x|

Decoder-only is actually a Encoder architecture, but used causual mask to let model predict next token based on previous tokens. 

**Causual mask** is not only a traing trick but also is embedded in the nature of Decoder-only architecture. So embedding of each token is only determined by itself and its previous tokens. (Foundation of KV-cache)

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


Based on **Natural Language Generation(NLG) trick**. Use text generation to pretrain the model and use text generation to reform other NLP tasks.

```bash

# Classifier reform
"The movie was fantastic!" => "Positive" 
# Reform to :
Input:  "The movie was fantastic! Sentiment: "
Output: "The movie was fantastic! Sentiment: Positive"

```
## Theory behind LLM

### Scaling law

| Year | Model Name / Version | Number of Parameters | Training Tokens |
| :--- | :--- | :--- | :--- |
| 2020 | GPT-3 (OpenAI) | 175B | 500B |
| 2023 | **Llama 2** (Meta) | 7B, 13B, 70B | 2T |
| 2023 | GPT-4 (OpenAI) | ~1.76T (Est. MoE) | N/A (Est. ~13T) |
| 2023 | Deepseek Coder (V1) | 1.3B, 6.7B, 33B | 2T |
| 2024 | **Llama 3.x** (Meta) | 1B, 3B (Text),8B, 70B, 405B  | 15T |
| 2024 | Qwen 2 (Alibaba) | 0.5B, 1.5B, 7B, 57B (MoE), 72B | 3T+ |
| 2025 | **Llama 4** (Meta) | Scout (109B), Maverick (400B) | N/A |
| 2025 | Deepseek V3 | 671B (MoE, 37B,  active) | > 4T |

Modern(2025) LLM normally has a context window of 128K, Llama4 has 1~10M.

### Context window
- Theoretical Possibility: It's theoretically possible to greatly extend the context window using improved PE design.

- Main Limitation: A model's useful context window is a balance between what it learned from its **training data**, and what is affordable given **hardware costs**, considering the optimize attention mechanism rather than native $O(n^{2})$ MHA .

- The Problem with Evaluation: There's no standard way to measure this capability. The large context numbers advertised by companies are more like a statement of potential or a system specification, not a guarantee of consistent performance on all long-text tasks.

### Emergent Properties

About Emergent Properties, there are two aspect:
- As to the **training process**, model reaches its bottleneck on training set performance but increased its generalizaiton ablity "suddenly".
- As to the **model capacity**, large model gains significant abilities which small models can not have. Or in a more dynamic way, some complex model functionality get suddenly improved from unable to capable respect to increasing of model capacity.

see `emergent_properties.md` for details.


## Tech based on LLM

### Chatbot

How is ChatGPT built: `chatGPT.md`.

### Prompt engineering

See `prompt_engineering.md`

### RAG
refer to `RAG.md`.

### Reasoning AI

