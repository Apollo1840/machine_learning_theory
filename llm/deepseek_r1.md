# How to build Deepseek R1

## Four key steps:

SFT $\rightarrow$ RL $\rightarrow$ SFT $\rightarrow$ RL

### SFT on CoT

Fine-tuning the base model on a small amount of high-quality, human-readable "long CoT" data.


### RL on reasoning (in reasoning-demand senario)

The model then undergoes large-scale RL focused on tasks like coding, math, and logic. 

- A key addition here is a "language consistency reward" to prevent the model from mixing languages in its responses.

### SFT on General purpose

Dataset:
- non-reasoning data (~200k samples)
- good model generated reasoning data (~600k samples) (rejection sampling). 


### RL on human preference

Using a combination of rule-based rewards for reasoning tasks and reward models for general queries.
