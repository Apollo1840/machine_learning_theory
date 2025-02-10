# Neural Network Basics
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28ML.one%7Ce8b3e705-493c-431b-b04e-8e9e3752864d%2F07-NeuroNetwork%7C02a354b1-68be-4afe-ac68-241c18b29aab%2F%29&wdorigin=NavigationUrl

## Task head

- regression:
  - Vanilla: for regression, probablistic regression.
  - ReLU and Softplus: positive regression.
- classification:
  - Softmax: single-label probability distribution, normalize **logits** to get values between 0 and 1.
  - Sigmoid: multi-label probability distribution.

  
## Losses
- mse
- entropy
    - binary cross-entropy
    - categorical cross-entropy
- Negative Log-Likelihood Loss (nll)
- focal loss
- triplenet loss
- similarity loss
- KL divergence

### KL divergence

Kullback-Leibler (KL) divergence is a measure of how one probability distribution P differs from a second probability distribution Q.
It quantifies the information loss when Q is used to approximate P. KL divergence is asymmetric and is defined as:

$$
D_{KL}(P \| Q) = \sum_{x} P(x) \log \frac{P(x)}{Q(x)}
$$

$$
D_{KL}(P \| Q) = \int p(x) \log \frac{p(x)}{q(x)} dx
$$

### NLL loss

```python

def gaussian_nll_loss(y_pred, y_true):
    mean, logvar = y_pred  # Model outputs mean and log-variance
    var = torch.exp(logvar)  # Convert log-variance to variance
    return torch.mean(0.5 * (logvar + (y_true - mean) ** 2 / var))  # NLL loss

```

## Optimizers

### Adam
When using Adam, we will keep the momentum of the gradient(u) and the momentum of the gradient square(v).

Instead of using the gradient, Adam used u and the u is scaled by the square root of v.

## Advances

### Normalization
- **BatchNorm**: Every feature is normalized independently across a batch.
- **LayerNorm**: Every feature of a single layer with a single input is normalized across each other.
- **InstanceNorm**: (Similar to LayerNorm) Every feature of a single layer with a single input is normalized across each other within one channel.
- **GroupNorm**: Grouped instanceNorm, ie. some channels are grouped.

(P.S. In the inferencing stage of a BatchNorm, the moving average during training is used, instead of the inferencing batch)

### Dropout

Randomly deactivate a fraction of neurons of a layer whenever tensor pass forward during the training phase.

It prevents the network from becoming overly reliant on specific neurons, thus promoting the learning of more robust and general features and reducing overfitting.

### Skip connection
Skip connection is a concept used in neural networks. It allows the model to bypass one or more layers by feeding the output of one layer directly into another layer further down the network.
- ( <-- ) It provides shorter paths for gradients to flow through the network, maintaining stronger gradients for early layers, and facilitating deeper deep learning.
- ( --> ) on the other hand, it allows the model to leverage both shallow and deep representations of the data, hence benefiting the performance and accelerating training in some cases.

### Training
- Vanishing gradient: gradient values are too small, and the related neuros fail to learn and update. It often caused by tanh saturation or too long backpropagation chains.
- Exploding gradient: gradient values are too big and the training process become unstable. It often happen with loss like MSE, when gradient positive related to weights, and it often caused by too large weights, large gradient accumulation or too large learning rate.

to avoid them, we can use:
- gradient clip.
- proper weight initialization and activation.
- skip connection.
- batch normalization (to prevent too-high or too-low input).