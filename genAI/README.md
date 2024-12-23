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

The methodology is developed from VAE, GAN to diffusion models, transformers.

## Text Generation
Transformers are dominating the field.

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
- Spectral generation: mostly Mel, first use model to generate the Mel, then use Vocoder to transform Mel into wave form.
- End-to-end: directly generate the waveform.


#### Tacotron

A standard model is **Tacotron**. 
Tacotron is a spectral generator, it has two parts:
- Text-to-Mel model: very like transformer-based translator.
- Mel-to-Waveform model (vocoder)

#### WaveNet

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

- Point-cloud
- Mesh (vertex and face)