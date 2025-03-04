# Generative AI

## Overview

### Modality
- Text
- Audio
- Image
- Video
- 3D structure: Mesh, point cloud

### Guidance

GenAI is developed from guide-free to text-guided.

```bash

Guide-free -> Class guided -> text guided

```
So it is strong connected to multi-modal learning nowadays.

### Methodology

Reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0-%E8%87%AA%E7%9B%91%E7%9D%A3%E5%AD%A6%E4%B9%A0.one%7Cbc0a5402-dd19-445e-b1c4-77c46195e6f7%2F%E7%94%9F%E6%88%90%E5%BC%8F%E6%A8%A1%E5%9E%8B%7C5ec031da-0616-47fc-a778-3c13dec3dfe4%2F%29&wdorigin=NavigationUrl

- Autoregressive models: PixelCNN/PixelRNN, GPT.
- VAE
- GAN
- Diffusion models
- Flow models: RealNVP/Glow

## Text Generation
Transformers are dominating the field.

Speech-to-Text(STT): Mozilla Deep Speech

## Image Generation
Most research area, with diffusion models dominating the field

## Audio Generation
### Application
- Text-to-speech(TTS)
- Music generation
- Sound effect generation (BGM/specific sound)
- Sound style transfer

### Standard methods
- Parameters generation: use parameterized synthesizer to generate the sound
- Spectral generation: mostly **Mel**, first use model to generate the Mel, then use Vocoder to transform Mel into wave form.
- End-to-end: directly generate the waveform.


#### Tacotron

A standard model is **Tacotron**. 
Tacotron is a spectral generator, it has two parts:
- Text-to-Mel model: very like transformer-based translator.
- Mel-to-Waveform model (vocoder)

#### WaveNet

**Vocoder**: Mel -> Waveform

A standard vocoder is the famous **WaveNet**.

WaveNet is a model that generates audio waveforms point by point.
During training, it takes an existing waveform segment as input and aims to predict each sample value while learning the distribution of audio signals.
In inference, WaveNet starts from an initial point (which could be a random value or derived from conditional information) and recursively generates a complete waveform point by point. 

Details in `wave_net.md`

## Video Generation

### VideoGAN
- Generator: RNN for the time axis hidden state generation, Deconv layers for the frame generation.
- Discriminator: mainly based on 3D convolution.

### Video-LDM
Based on diffusion models.

## 3D model Generation

### Application

- Voxel
- Point-cloud
- Mesh (vertex and face)
- Implicit Representation (NeRF)

### Standard methods

#### Voxel generation

3D-GAN based on 3D convolution.

#### Point cloud generation

PointFlow: based on VAE and flow model.

Procedure:
- Use VAE and Pooling to compress points into a hidden vector - cloud embedding.
- Based on cloud embedding, use a flow model to generate points one by one.
- While inferencing, we can simplify just sample a cloud embedding to start.

Details:
- The cloud embedding is generated from a VAE, so it is not only an embedding, but also a distribution around it. 
  That is also why a flow model can be trained here to generate points of another imaginary distribution.
- End criterion: fixed N or probability threshold.

#### Mesh generation

AtlasNet: A cloud points guided mesh generator, with the help of a 2D grid. 

- Input: cloud points.
- Output: a Mesh (V, F. Set of vertics and faces)

Procedure:
- cloud points is encoded into a cloud embedding.
- the embedding guide the 2D-grid to project to the cloud points, use chamfer loss to train the projector.
- define the faces on the 2d-grid and the grids are defined as vertices.

### Advanced methods
- 3DGen: from Meta, combine NeRF and diffusion models. (https://scontent-muc2-1.xx.fbcdn.net/v/t39.2365-6/449707112_509645168082163_2193712134508658234_n.pdf?_nc_cat=111&ccb=1-7&_nc_sid=3c67a6&_nc_ohc=4P16BvvLQIgQ7kNvgEnaDTl&_nc_zt=14&_nc_ht=scontent-muc2-1.xx&_nc_gid=Ah3_D4TDJt5eqXiKIhGW2Qh&oh=00_AYD9V_A0r8PLTwclmlkvkBxTU646TQDHExABMOJHut0nUg&oe=676F4511)
- Shap-E: from OpenAI, use implicit representation as well, but is a mesh generator (https://github.com/openai/shap-e)
- TPA3D: based on GAN.