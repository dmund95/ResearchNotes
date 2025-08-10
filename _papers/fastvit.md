---
layout: paper
title: "FastViT"
authors: []
year: 2023
journal: ""
paper: https://arxiv.org/pdf/2303.14189
---

## Summary

Efficient network for on device image processing. Inspired by ViT architecture and hence the name. This is a hybrid architecture with attention and CNN layers. However it heavily uses CNN layers and attention is only used at the final block.

There are three key design choices.
1. Introduces RepMixer module. However this is just a simple skip connection module. The novelty is using reparameterization trick at inference to avoid skip connection and reduce memory access cost
2. Train time over-parameterization. This is similar to MobileOne architecture where multiple branches with different sized conv kernels are used at training and at inference are merged into a single conv layer.
3. Since the paper avoids using self attention in all blocks (except last) which is a costly operation, to keep similar receptive field, large kernel sizes are used in early layers. 

<figure class="image-container">
    <img src="{{ '/assets/images/fastvit.png' | relative_url }}" alt="FastVIT architecture" class="paper-image">
    <figcaption class="image-caption">FastVIT architecture</figcaption>
</figure>