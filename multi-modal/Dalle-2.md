# DALL-E 2

Dalle-2 is a very good milestone to understand multi-modal learning.

DALLE-2 is a text-guided image generator. 
Similar to **Stable diffusion**, image generation is manupilated(denosing) on latent space. (So there is an Image encoder). 
Dalle-2 has the following key innovations:
- (**Aligned space**) Instead of using independent image and text encoder, it uses a text-image unified model - CLIP.
- (**Upsampling**) Use upsampling trick to generate high resolution image.

