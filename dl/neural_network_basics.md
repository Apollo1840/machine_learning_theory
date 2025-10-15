# Neural Network Basics
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28ML.one%7Ce8b3e705-493c-431b-b04e-8e9e3752864d%2F07-NeuroNetwork%7C02a354b1-68be-4afe-ac68-241c18b29aab%2F%29&wdorigin=NavigationUrl

## Connection


### MLP & FFN & Bottleneck FFN
- MLP: Multi-layer neuro network.
- FFN: One **larger** layer = two linear project with one activation in-between. 
- Bottleneck FFN: One **smaller** layer.

### Skip connection
Skip connection is a concept used in neural networks. 
It allows the model to bypass one or more layers by feeding the output of one layer directly into another layer further down the network.
- ( --> ) it allows the model to leverage both shallow and deep representations of the data, hence benefiting the performance and accelerating training in some cases.
- ( <-- ) on the other hand, it provides shorter paths for gradients to flow through the network, maintaining stronger gradients for early layers, and facilitating deeper deep learning.


## Activation

- ReLU
- Sigmoid
- Softmax
- Tanh
- LeakyReLU
- Softplus: $\log(1+\exp(-z))$
- ELU
- GELU
- SiLU
- SwiGLU(A complex gate)

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
    - binary cross-entropy (BCE)
    - categorical cross-entropy (CCE)

(Here we just listed and introduce some basic losses. For wider understanding, go to `./losses.md`.)

Binary cross-entropy (BCE):

$$
\mathcal{L}_{BCE} = -\frac{1}{N} \sum_{i=1}^{N} \sum_{c=1}^{C} [ y_{i,c} \log(\hat{y}_{i,c}) + (1 - y_{i,c}) \log(1 - \hat{y}_{i,c})]
$$

Categorical cross-entropy (CCE):

$$
\mathcal{L}_{CCE} = -\frac{1}{N} \sum_{i=1}^{N} \sum_{c=1}^{C} y_{i,c} \log(\hat{y}_{i,c})
$$

A important note is that: when softmax come with the CCE loss, the gradient is simply $y - \hat{y}$. Whereas, if we use MSE to replace CCE, 
it will be $(y - \hat{y})(1 - \hat{y})\hat{y}$, gradient will be very small close to 0 and 1. 


## Optimizers

### SGD
- sensitive to noise -> Oscillation
- slow on flat area.

**Learning rate**: step length along the gradient direction. 

**batch size**: sampling size of the data points to enable mini-batch SGD.

### Adam
When using Adam, we will keep the:
- u: momentum of the **gradient** and 
- v: momentum of the **gradient square**.

Instead of using the gradient, Adam used u and the u is scaled by the square root of v.

In Adam, learning rate is more like maximum of step length. actual 'learning rate' is adaptive to the variance of the gradient. 


### AdamW

**Weight decay**: when update the parameters, also minus a scaled value of the parameter. In SGD, weight decay is essential equal to L2 regulariation.

AdamW implements decoupled weight decay. This provides the desired regularization effect of L2 without interfering with Adam's adaptive learning rate mechanism, leading to better performance.

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

- **Vanishing gradient** (gradient values are too small, and the related neuros fail to learn and update) 
  
  Cause: It can be derived that the gradient is positive relate to weights. So bad initialization can cause earlier layers have zero gradient because of the too long backpropagation chain. (Same for exploding gradient). And it also can be caused by activation saturation like tanh.

- **Exploding gradient** (gradient values are too big and the training process become unstable)
  
  Cause: As above. And losses like MSE make gradient positive to the discrepancy, so it can make the situation worse in the starting point.

to avoid them, we can use:
- gradient clip.
- proper weight initialization and activation, like Xavier.
- skip connection.
- batch normalization (to prevent too-high or too-low activation, resulting in too-high or too-low last term of the formula).


An important insight is that:
- Gradient are outter product of input and discrepancy. 


## Weight initialization

### Xavier

$$
W \sim U\left[-\frac{\sqrt{6}}{\sqrt{n_{in} + n_{out}}}, \frac{\sqrt{6}}{\sqrt{n_{in} + n_{out}}}\right]
$$

or

$$
W \sim \mathcal{N}\left(0, \sqrt{\frac{2}{n_{in} + n_{out}}}\right)
$$

## Advances

### Special Nets
- cnn, see `../cv/cnn.md`.
- rnn, see `../nlp/rnn.md`.
- gnn, see `./gnn.md`.
- transformer `../transformer/README.md`