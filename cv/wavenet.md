# WavNet

WavNet is designed for audio generation and belongs to the Temporal Convolution Network(TCN).

It utilizes dilated causal convolution layers to process the signal data in an auto-regressive way, meaning that each neuro can see the inputs before that time stamp. Using dilated causal convolutions to skip over some inputs for each layer, it allows the network to have a large receptive field.