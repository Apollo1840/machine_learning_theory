# Advanced Deep Learning

## Transfer learning
It is a model **weights initialization** technique. 
A model trained for one task is reused as the starting point for a model on another related task.

see `transfer_learning.md` in details.

### few-shots learning
Train models with very limited amount of training samples, often just one or a few.

Typically through transfer learning. A pretrained model is used to generate the embedding of the data and a trivial model (eg. a distance-based model) is used to accomplish the task.

## Robust AI
see `robust.md`.

## Efficient AI
There two aspects of this topic:
- make model smaller (with **reasonable** cost of performance)
- make big model more efficient (with **minimum** cost of performance)

### lower resource design
see `model_efficiency.md`, `model_distillation.md`.

### minimum-cost design (Edge AI)
see `model_distillation.md`.

Also includes smart split of task between local model and remote big model service.