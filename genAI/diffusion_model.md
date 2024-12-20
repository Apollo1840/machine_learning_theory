# diffusion model

reference: 
- paper: https://arxiv.org/pdf/2006.11239
- implementation: https://github.com/awjuliani/pytorch-diffusion/tree/master

## Denoising Diffusion Probabilistic Models (DDPM)

In a diffusion model development, a model is trained to predict the noise participant of a noisy image, 
given its noising step number.

```python
# pseudo code of core train_step

for x, _ in dataloader:
    noise = randn()
    noisy_xs = add_noise(x, ts, noise)
    y = model(noisy_xs, ts)
    
    loss = mse_loss(y, noise)
    # ...
```

### Noising(for train) and Denoising(for inference) details

$\beta_t$ is the noise variance schedule, 
a predefined sequence of small positive numbers $\beta_t \in (0, 1)$. 
It defines how much noise is added at each step $t$ in the forward diffusion process. 
It serves as the foundation for defining $\alpha_t$ and $\bar{\alpha}_t$.


- $\alpha_t = 1 - \beta_t$
- $\bar{\alpha}\_t = \prod_{i=1}^t \alpha_i = \prod_{i=1}^t (1 - \beta_i)$

$$
\mathbf{x}_t = \sqrt{\bar{\alpha}_t} \mathbf{x}_0 + \sqrt{1 - \bar{\alpha}_t} \mathbf{\varepsilon}
$$
where $\mathbf{\varepsilon} \sim \mathcal{N}(0, I)$

Reverse process (inference): 
$$
\mathbf{x}_{t-1} = \frac{\mathbf{x}\_t - \sqrt{1 - \bar{\alpha}\_t} \mathbf{\varepsilon}\_\theta(\mathbf{x}\_t, t)}{\sqrt{\alpha_t}} + \sigma_t \mathbf{z}
$$
where:
- $\mathbf{\varepsilon}\_\theta$ is the model's predicted noise.
- $\sigma_t = \sqrt{\beta_t}$ is added noise for stochasticity.

---

## Summary
- **\(\beta_t\)**: Defines the noise added at each step.
- **\(\alpha_t\)**: Fraction of signal retained at a single step (\(\alpha_t = 1 - \beta_t\)).
- **\(\bar{\alpha}_t\)**: Fraction of signal retained cumulatively across steps (\(\bar{\alpha}_t = \prod_{i=1}^t \alpha_i\)).

This framework ensures a consistent forward and reverse diffusion process.
