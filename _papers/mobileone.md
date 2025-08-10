---
layout: paper
title: "MobileOne"
authors: []
year: 2023
journal: ""
paper: https://arxiv.org/pdf/2206.04040
---

## Summary

The paper proposes an efficient network architecture.

## Key ideas

1. Authors notice that FLOPs and parameter count do not directly correlate with on device latency. For example, models with highly shared parameters can have huge latency (think transformers) and FLOPs does not account for memory access cost / parallelism
2. Authors notice that branching and skip connections like in ResNet are not favourable for latency since previous activations need to be stored and fetched to compute downstream activations
3. Mainly focused on Depthwise separable convolution technique introduced in MobileNet. 
4. Use train-time over-parameterization to train a more scalable model. At inference, the network is re-parameterized (like in RepVGG) as a single Conv block with no branching. 
5. Two types of train-time over-parameterization:
   1. Linear over-parameterization: (Conv + BN) blocks sequentially added. Overall the operation can still be represented as a single conv layer but increase in parameters during training makes it easier for the model to search solution space
   2. Branching over-parameterization: (Conv + BN) blocks in parallel connection. Overall the operation can be written as sum of Weight and bias terms. 
6. In depth-wise convolution, a 3x3 depthwise conv is followed by a 1x1 channelwise conv. The authors introduce over-parameterization in both the blocks.
7. The usual sequence of blocks is Conv-Relu-BN. The structure is changed to Conv-BN-Relu so as to enable re-parametrization trick 

<figure class="image-container">
    <img src="{{ '/assets/images/mobileone.png' | relative_url }}" alt="MobileOne reparametrization trick" class="paper-image">
    <figcaption class="image-caption">MobileOne reparametrization trick</figcaption>
</figure>