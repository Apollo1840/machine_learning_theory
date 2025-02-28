# Neural Network Basics
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28ML.one%7Ce8b3e705-493c-431b-b04e-8e9e3752864d%2F07-NeuroNetwork%7C02a354b1-68be-4afe-ac68-241c18b29aab%2F%29&wdorigin=NavigationUrl

## Connection
### Skip connection
Skip connection is a concept used in neural networks. 
It allows the model to bypass one or more layers by feeding the output of one layer directly into another layer further down the network.
- ( --> ) it allows the model to leverage both shallow and deep representations of the data, hence benefiting the performance and accelerating training in some cases.
- ( <-- ) on the other hand, it provides shorter paths for gradients to flow through the network, maintaining stronger gradients for early layers, and facilitating deeper deep learning.


## Task head

- regression:
  - Vanilla: for regression, probablistic regression.
  - ReLU and Softplus: positive regression.
- classification:
  - Softmax: single-label probability distribution, normalize **logits** to get values between 0 and 1.
  - Sigmoid: multi-label probability distribution.
- generation: Introduced in specific fields.

  
## Losses
- MSE
- Entropy
    - cross-entropy (CE)
      - binary cross-entropy
      - categorical cross-entropy
    - Negative Log-Likelihood Loss (NLL)
    - focal loss 
- Alignment loss
  - distance-based
      - siamese contrastive loss
      - triplenet loss
  - softmax similarity-based
    - InfoNCE Loss
    - NT-Xent Loss
  - KL divergence

### Entropy loss

### NLL loss

The Negative Log-Likelihood (NLL) Loss is a commonly used loss function in classification tasks, particularly in probabilistic models.

$$
\mathcal{L} = -\log p_{\theta}(y | x)
$$

When applied to a classification problem with a softmax output layer, NLL loss is equivalent to cross-entropy loss.

#### Gaussian NLL loss
Gaussian Negative Log-Likelihood (Gaussian NLL Loss) is a loss function used for probabilistic regression, 
where the model predicts both the **mean** and **variance** of a Gaussian (Normal) distribution. This allows the model to express uncertainty in predictions.

```python

def gaussian_nll_loss(y_pred, y_true):
    mean, logvar = y_pred  # Model outputs mean and log-variance
    var = torch.exp(logvar)  # Convert log-variance to variance
    return torch.mean(0.5 * (logvar + (y_true - mean) ** 2 / var))  # NLL loss

```


#### Focal loss

Focus more on less-presented and miss-classified samples.
Often used in imbalanced classification cases.

$$
FL(p_t) = -\alpha_t (1 - p_t)^\gamma \log(p_t)
$$

### Alignment loss

#### InfoNCE
Push the prefect matching between `q` and the correct `k0`.

$$
\mathcal{L}\_{\text{InfoNCE}} = -\log \frac{\exp (q \cdot k_0 / \tau)}{\sum_{i=0}^{N} \exp (q \cdot k_i / \tau)}
$$

Generalization of InfoNCE if the target is a similiarity matrix:

$$
\mathcal{L}\_{\text{img2txt}} = - \frac{1}{N} \sum_{i=1}^{N} \log \frac{\exp (S_{ii} / \tau)}{\sum_{j=1}^{N} \exp (S_{ij} / \tau)}
$$

`S_ij` is the similarity between the image and all text embeddings in the batch.

#### KL divergence

Kullback-Leibler (KL) divergence is a measure of how one probability distribution P differs from a second probability distribution Q.
It quantifies the information loss when Q is used to approximate P. 

KL divergence is asymmetric and is defined as:

$$
D_{KL}(P \| Q) = \sum_{x} P(x) \log \frac{P(x)}{Q(x)}
$$

$$
D_{KL}(P \| Q) = \int p(x) \log \frac{p(x)}{q(x)} dx
$$

Often used as:
- Probabilistic distribution approximation
- Regularization

P.S. Related to Jensen-Shannon Divergence (JSD)


## Optimizers

### Adam
When using Adam, we will keep the:
- u: momentum of the **gradient** and 
- v: momentum of the **gradient square**.

Instead of using the gradient, Adam used u and the u is scaled by the square root of v.


### Training
#### reference
  - (BP) https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0.one%7C4ab3a169-69c4-42b8-b4ff-6611a9ee8a28%2F%E6%97%A0%E6%A0%87%E9%A2%98%E9%A1%B5%7C3ef70319-df8e-4bd4-89e8-f925613ed0af%2F%29&wdorigin=NavigationUrl
  - (BP) https://www.youtube.com/watch?v=yXcQ4B-YSjQ&list=PLkDaE6sCZn6Ec-XTbcX1uRg2_u4xOEky0&index=34&ab_channel=DeepLearningAI
  - (Gradient vanish/exploding)  https://www.youtube.com/watch?v=qhXZsFVxGKo&ab_channel=DeepLearningAI

#### Backprop

$$
\frac{\partial L}{\partial w^{(i)}} = \frac{\partial L}{\partial y} \cdot \prod_{j=i}^{N} \frac{\partial h_{j+1}}{\partial h_j} \cdot \frac{\partial h_i}{\partial w^{(i)}}
$$

This formula describes how to calculate gradient of the weights in each layer. 
To calculate the middle term, we use DP method, hence we maintain the intermediate result and pass it (with update) 
to the former layer, and this is so called back-propagation.

Since we have a long chain of multiplication if the NN is deep. So problems like gradinet vanish/exploding might happen:

- Vanishing gradient (gradient values are too small, and the related neuros fail to learn and update) 
  
  Cause: Too long backpropagation chains and bad initialization. And it also often caused by tanh saturation.

- Exploding gradient (gradient values are too big and the training process become unstable)
  
  Cause: Too long backpropagation chains and bad initialization. And it often happen with loss like MSE, when gradient positive related to weights, and it often caused by too large learning rate.

to avoid them, we can use:
- gradient clip.
- proper weight initialization and activation.
- skip connection.
- batch normalization (to prevent too-high or too-low activation, resulting in too-high or too-low last term of the formula).

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

### Special Nets
- cnn, see `../cv/cnn.md`.
- rnn, see `../nlp/rnn.md`.
- gnn, see `./gnn.md`.
- transformer `../transformer/README.md`