
# Losses

"losses is more than how you quantify your model outputs to the target. It is essentally about how you model your problem."

## Basic concepts

### Kullback-Leibler (KL) Divergence

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


A useful formula:
$$
D_{KL}(p || q) = \sum p \log \frac{p}{q} = \sum p \log p - \sum p \log q = H(p, q) - H(p)
$$


### Maximum Likelihood Estimation (MLE) &  Negative Log-Likelihood (NLL)

The goal of MLE is to find the parameters $\theta$ that make the observed data "most probable."

For our entire dataset $\\{ (x^{(i)}, y^{(i)}) \\}_{i=1}^{N}$, the likelihood $L(\theta)$ is:

$$
L(\theta) = P(Y | X; \theta) = \prod_{i=1}^{N} P(y^{(i)} | x^{(i)}; \theta)
$$

It's often easier to work with sums than products. We take the negative logarithm, giving us the **Negative Log-Likelihood (NLL)**:

$$
-\log L(\theta) = -\sum_{i=1}^{N} \log P(y^{(i)} | x^{(i)}; \theta)
$$

**We often use NLL as our loss function, $J(\theta)$.** Minimizing this loss is *equivalent* to maximizing the likelihood.

$$
\min_{\theta} NLL = \max_{\theta} L
$$

### Basic losses

#### Mean Squared Error (MSE)

The **MSE** is just the SSE divided by the number of samples $N$:
$$
\text{MSE} = \frac{1}{N} \sum_{i=1}^{N} (y^{(i)} - \hat{y}^{(i)})^2
$$

##### Gaussian NLL loss
It is a loss function used for probabilistic regression, 
where the model predicts both the **mean** and **variance** of a Gaussian (Normal) distribution. This allows the model to express uncertainty in predictions.

```python

def gaussian_nll_loss(y_pred, y_true):
    mean, logvar = y_pred  # Model outputs mean and log-variance
    var = torch.exp(logvar)  # Convert log-variance to variance
    return torch.mean(0.5 * (logvar + (y_true - mean) ** 2 / var))  # NLL loss

```


#### Mean Absolute Error (MAE)

$$
\text{MAE} = \frac{1}{N} \sum_{i=1}^{N} | y^{(i)} - \hat{y}^{(i)} |
$$


#### (Categorical) Cross Entropy (CCE)

$$
\mathcal{L}_{CCE} = -\frac{1}{N} \sum_{i=1}^{N} \sum_{c=1}^{C} y_{i,c} \log(\hat{y}_{i,c})
$$

Work with Softmax activation.


##### Focal loss

Focus more on less-presented and miss-classified samples.
Often used in imbalanced classification cases.

$$
FL(p_t) = -\alpha_t (1 - p_t)^\gamma \log(p_t)
$$

Insight: gradient of dominating examples get scaled down. $\alpha_t$ is an additional weight.

#### Binary Cross Entropy (BCE)

$$
\mathcal{L}_{BCE} = -\frac{1}{N} \sum_{i=1}^{N} \sum_{c=1}^{C} [ y_{i,c} \log(\hat{y}_{i,c}) + (1 - y_{i,c}) \log(1 - \hat{y}_{i,c})]
$$

Work with Sigmoid activation.

When they are multiple target which can co-appear, ie. multi-label classification. Simply treat each target as a new loss and aggregate them by sum (as shown in the formula).

### Advanced losses

#### Alignment loss

- distance-based
    - siamese contrastive loss
    - triplenet loss
- softmax similarity-based
  - InfoNCE Loss (NT-Xent)
  - Symmetric Cross-Entropy

##### Siamese Contrastive Loss
For positive pair $(x_i, x_j)$ and negative pairs $(x_i, x_k)$:
$$
\mathcal{L}_{\text{contrastive}} = \frac{1}{2N} \sum_{n=1}^N \left[ y d(x_i, x_j)^2 + (1-y) \max(0, m - d(x_i, x_k))^2 \right]
$$
where $y=1$ for positive pairs, $y=0$ for negative pairs, $m$ is margin, $d$ is distance metric.

##### Triplet Loss
For anchor $a$, positive $p$, negative $n$:
$$
\mathcal{L}_{\text{triplet}} = \max(0, d(a,p) - d(a,n) + m)
$$

##### InfoNCE
Push the prefect matching between `q` and the correct `k0`. Lets assume they are vectors and we can use $q \cdot k_0$ to measure the similarity; and we have only two other `k`s: `k1`,`k2`.

The loss could look like this:

$$
\mathcal{L} = -\log \frac{\exp (q \cdot k_0)}{\exp (q \cdot k_0) + \exp(q \cdot k_1) + \exp(q \cdot k_2)}
$$


InfoNCE is with temperature $\tau$.

$$
\mathcal{L}_{\text{InfoNCE}} = -\log \frac{\exp (q \cdot k_0 / \tau)}{\sum_{i=0}^{N} \exp (q \cdot k_i / \tau)}
$$

Generalization of InfoNCE if the target is a similiarity matrix:

$$
\mathcal{L}_{\text{img2txt}} = - \frac{1}{N} \sum_{i=1}^{N} \log \frac{\exp (S_{ii} / \tau)}{\sum_{j=1}^{N} \exp (S_{ij} / \tau)}
$$

`S_ij` is the similarity between the image and all text embeddings in the batch.

##### Symmetric Cross-Entropy
For similarity matrix $S$ where $S_{ij} = \text{sim}(x_i, y_j)$:
$$
\mathcal{L}_{\text{sym}} = \frac{1}{2N} \sum_{i=1}^N \left[ -\log \frac{\exp(S_{ii}/\tau)}{\sum_j \exp(S_{ij}/\tau)} -\log \frac{\exp(S_{ii}/\tau)}{\sum_j \exp(S_{ji}/\tau)} \right]
$$

## Theories



### NLL and MSE
In regression, we assume a continuous target variable $y$. The most common assumption is that the error between our prediction $\hat{y}$ and the true value $y$ is distributed according to a **Gaussian (Normal) distribution** with zero mean and some variance $\sigma^2$.

Under this assumption, with NLL we can get MSE which is possitive correlated to NLL.


### NLL and MAE
In regression, if we assume noise be Laplacian, then the loss can be MAE.

### NLL and CCE
In classification, if we use Bernoulli probablistic model then we can write the model as:

$$
P(y | x; \theta) = \prod_{j=1}^{K} \hat{y}_j^{\, y_j}
$$
where $y$ is a **one-hot encoded** vector.

If so, we can use this model to get CCE.

### CCE and KL-divergence

Minimizing the Cross-Entropy is identical to minimizing the KL Divergence between the true label distribution and the predicted distribution.
   
### Gradient Behavior
The combination of final-layer activation (Linear for MSE, Sigmoid/Softmax for Cross-Entropy) and its corresponding loss function leads to **well-behaved gradients**.
   - For Binary Cross-Entropy with Sigmoid: $\frac{\partial J}{\partial z} = \hat{y} - y$ (simple, non-vanishing gradient)
   - Using MSE with Sigmoid would include $\hat{y}(1-\hat{y})$ in the gradient, which can vanish when the neuron is saturated.

## Practice

In real cases, loss curve can be unstable. Mostly because gradient exploding. Typical solutions are:
- Gradient clip
- LR warmup




