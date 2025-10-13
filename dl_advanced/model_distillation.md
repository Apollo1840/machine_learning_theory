# Model distillation

## Knowledge distillation(KD)
It is an advanced label smoothing technique, where the hard label is replaced by probablistic distribution from a teacher model. 

- The student model is typically smaller than teacher, hence KD can be regarded as a model compression method.
- The loss is typically a combined loss of hard target and soft target.

### Advanced KD
- FitNets, not only target, but also the intermediate features is guided.
- Attention transfer(AT), guide the student via attention map preview. (https://arxiv.org/pdf/1612.03928)