---
layout: paper
title: "MobileCLIP"
authors: []
year: 2024
journal: ""
paper: https://arxiv.org/pdf/2311.17049
---

## Summary

Basically a faster version of CLIP models that are edge device friendly.

## Key ideas

1. The architecture for text and image encoders are heavily based on FastViT. The main idea is to use large convolutions in the shallower layers and later layers use self attention. 
2. These architectures are designed to be low latency and memory consuming which can be deployed on mobile devices. 
3. To train these models, authors use ensemble of large CLIP models to generate text and image embeddings. The knowledge is distilled to the smaller models using this augmented dataset. The loss function is weighted sum of usual CLIP loss (contrastive loss within batch) and distillation loss (force the embeddings learnt by student model are similar to teacher embeddings) 