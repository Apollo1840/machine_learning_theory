# Latent space learning
The NN learning to compress/encode the data to a guassian distribution.
This concept ususally used in field of deep generation 
and strongly related to the concept of normalizing flow (see `normalizing_flow.md`).

KL-divergence loss is a core concept.

## VAE

Encoder-Decoder

Loss = reconstruction_loss + KL_latent_to_gaussian

Important note:
- reparameterization(sampling latent) is important to ensure the smooth distribution of the latent space.

## Conditional VAE

Compare to VAE, condition is added to the input of Encoder and Decoder respectively.
Therefore, the latent vector is also based on condition.
