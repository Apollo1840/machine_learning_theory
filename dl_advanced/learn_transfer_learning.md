# Transfer learning

## Assumptions
- **Feature reusability**:  the features(or latent representation) learned from the source domain/task are useful for the target domain/task. Because of the **domain relation and task similarity**. 
- **Source dependability**: the source task should have sufficient data and a well-trained model so that the knowledge is valid.
- **Finetune consistency**: the finetune method ensure the model benefit from the learned feature, and has the ability to adapt to target domain.  

## Finetune techniques

### Standard finetune

#### Entire finetune
Unfrozen the all weights and treat weights of the pretrained model as weights initialization.

In Entire finetune, we tend to update the weights cautiously. For example, we use smaller LR overall or wisely, such as:

-  **Learning Rate Tuning**:
Use layer-specific learning rates during finetuning, assigning lower rates to earlier layers and higher rates to later layers. 

- **Cautious Updating**:
Use L2 or KL divergence to penalize changes to parameters.
  - **Elastic Weight Consolidation (EWC)**:
  Penalize changes to parameters deemed important (Fisher-Information matrix) for the pretrained model’s tasks. 

#### Partial finetune
Unfrozen specific layers (usually the last task head or last several laysers) and only updates theirs weights during the finetuning.

- **BitFit**:
Only update the **bias** terms of the pretrained model during finetuning, keeping all other parameters frozen. 


#### Proceduralized partial finetune
Dynamically unfrozen layers. For example, start by finetuning only the task head, then gradually unfreeze layers one by one. 

### Aggregated finetune

#### Aggregated layer
Add more layers (before/in-between/after) to the pretrained model and only finetune those layers.

Examples:
- (start) Adding domain-specific input reformers/encoders.
- (end) Adding task-specific classification heads.
- (middle) Integrating adapters within layers. such as **Adapter Tunning**, insert small bottleneck layers (adapters) into each layer of the pretrained model. During finetuning, only the adapter layers are updated, leaving the main model weights untouched.

#### Aggregated weights

- **Delta Tuning**:
We train a linear update of the weights ($\Delta w$), instead of direct change the weights. Note this is mathematically equivalent to direct finetune. However we can do various things upon the ($\Delta w$) and this idea is fundamental to understand more complex PEFT methods.

#### Aggregated token
Add task-specific prefix tokens to the input sequence. 
These tokens are learnable and serve to steer the model toward task-specific objectives without modifying the pretrained parameters.

### Parameter-efficient finetune (PEFT)

#### LoRA
Base on Delta Tuning, but use two low-rank matrix multiplications to represent $\Delta w$ and update those matrices instead of W.

$$
  W_{final} = W_{pretrained} + \Delta W \\
  \Delta W = A × B
$$

where 
- `A ∈ ℝ^(d×r)`, `B ∈ ℝ^(r×k)`
- Rank `r ≪ min(d,k)` (typically 4-64)
- Only `A` and `B` are trained, `W_pretrained` is frozen

in implementation, we just create LoRA supported layers like:

´´´python

    def forward(self, x):
        # Normal linear forward with frozen W
        result = F.linear(x, self.weight, self.bias)

        # Add the LoRA update
        if self.r > 0:
            lora_update = F.linear(x, self.A.T)      # (batch, r)
            lora_update = F.linear(lora_update, self.B)  # (batch, out_features)
            result += self.scaling * lora_update

        return result
´´´
