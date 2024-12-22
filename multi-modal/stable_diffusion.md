# Stable diffusion(SD)

SD is a text-guided image generator. 
The image generation is based on diffusion model, 
and there is a text embedding to guide the diffusion/generation process.

Works like GLIDE researched how to guide the diffusion process througn text embedding.
The innovation of SD is that: 
- the diffusion process happens in latent space. 
- the guide machnimus is a little different.

## Text Guide

In GLIDE(https://arxiv.org/pdf/2112.10741), the text embedding is just like time embedding,
it is add to the intermediate features of the UNet:

$$
h_t = h_t + \phi (t) + \Phi_\theta (t)
$$