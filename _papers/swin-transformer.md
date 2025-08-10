---
layout: paper
title: "Swin Transformer"
authors: []
year: 2021
journal: ""
paper: https://arxiv.org/pdf/2103.14030
---

## Summary

Introduces novel transformer based 2D back for image processing. Unlike ViT, the model can learn finer features at different scales (like VGG / ResNet) and has linear time complexity wrt image size

## Key ideas

1. Image is partitioned across different windows. Each window consists of MxM patches. Self attention only attends to patches inside a window. This ensures self attention time complexity does not blow up wrt image size 
2. However, since each patch will only attend to a fixed set of patches this limits the representation capacity of the model. To address this, strided window partition is used for the next layer. This is similar to DSVT architecture. This allows mixing of features across window partition.
3. To inject position information in self attention, the papers uses relative position bias. Instead of absolute position encoding appended to key / query features, learnt relative position scalar values are added to the attention matrix. 
4. Features are downsampled as the network goes deeper by merging patches. This ensures that at each stage, the network learns feature representation at different scales. Similar to ResNet. These features can be processed using FPN network for object detection or segmentation task. 

<figure class="image-container">
    <img src="{{ '/assets/images/swin.png' | relative_url }}" alt="Swin-Transformer overview" class="paper-image">
    <figcaption class="image-caption">Swin-Transformer overview</figcaption>
</figure>