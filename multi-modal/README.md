# Multi-modal learning


## Stage 1
It starts with image-text joint learning. eg:
- Image caption
- Vision QA

Works are focus on **feature fusion**:
- simple concatenation
- weighted sum
- Bilinear Interaction (https://arxiv.org/abs/1606.01847)


## Stage 2
With the raise of Transformer, 
people use transformer to unify the vision and language model.
with Contrastive Language–Image Pre-training(**CLIP**)(`./CLIP.md`) be a very good example.

With the raise of diffusion model and efficient latent space control. Image generation gets to a new milestone, 
hence comes a new form of vision and language model focus on AI generation (text-guided image generation). 
with **Stable Diffusion**(`stable_diffusion.md`) as a good example.


## Stage 3
Nowadays, people are trying to fusion more modals other than image and text. 
Embedding space alignment is a big topic here. 
works worthnoting are:
- VITA（https://arxiv.org/pdf/2408.05211): Mainly use **Contrastive learning** to align the embedding space. evolving tagging trick to operate different modals.
- MACAW-LLM (https://arxiv.org/pdf/2306.09093): Mainly use **Attention alignment**. Other modality embedding as Query and Language embeddding as Key and Values.

