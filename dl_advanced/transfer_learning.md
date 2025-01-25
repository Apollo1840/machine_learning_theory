# Transfer learning


## Finetune techniques

### Standard finetune

#### Entire finetune
Unfrozen the all weights and treat weights of the pretrained model as weights initialization.

- **Learning Rate Tuning**:
Use layer-specific learning rates during finetuning, assigning lower rates to earlier layers and higher rates to later layers. 
This aligns with the intuition that earlier layers contain general features, while later layers are more task-specific.

- **Elastic Weight Consolidation (EWC)**:
Penalize changes to parameters deemed important for the pretrained model’s tasks. 
This approach helps mitigate catastrophic forgetting, ensuring the model retains its original capabilities while adapting to new tasks.


#### Partial finetune
Unfrozen specific layers (usually the last task head or last several laysers) and only updates theirs weights during the finetuning.

- **BitFit**:
Only update the bias terms of the pretrained model during finetuning, keeping all other parameters frozen. This method reduces computational overhead significantly while retaining task performance.


#### Proceduralized partial finetune
Dynamically unfrozen layers. For example, start by finetuning only the task head, then gradually unfreeze layers one by one. 

### Aggregated finetune

#### Aggregated layer
Add more layers (before/in-between/after) to the pretrained model and only finetune those layers.

Examples:
- Adding task-specific classification heads.
- Adding domain-specific input reformers/encoders.
- Integrating adapters within layers. such as **Adapter Tunning**, insert small bottleneck layers (adapters) into each layer of the pretrained model. During finetuning, only the adapter layers are updated, leaving the main model weights untouched.

#### Aggregated token
Add task-specific prefix tokens to the input sequence. 
These tokens are learnable and serve to steer the model toward task-specific objectives without modifying the pretrained parameters.

### Parameter-efficient finetune

#### LoRA
Use two low-rank matrix multiplications to represent W and update those matrices instead of W.

note: W = A x B, A, B is learned through training, not decomposed from W after training.

