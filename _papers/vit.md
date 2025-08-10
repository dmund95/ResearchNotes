---
layout: paper
title: "ViT Vision-Transformer"
authors: []
year: 2021
journal: ""
paper: https://arxiv.org/pdf/2010.11929
---

## Summary

Seminal paper that introduces transformer only architecture for image processing tasks.

## Key ideas

1. Image of shape CxHxW is divided into patches of size PxP. Number of patches = (HxW/P**2)
2. The patched representation is considered as a 1D sequence of tokens. Just like in NLP transformers, each token is appended with a learnable 1D position embedding. Like in BERT a special learnable [CLS] token is appended at the beginning of each sequence that contains the information about the entire sequence.
3. The sequence of tokens are passed through standard transformer encoder blocks to learn per patch embeddings as well as overall [CLS] embeddings, which are used for class prediction task 

<figure class="image-container">
    <img src="{{ '/assets/images/vit.png' | relative_url }}" alt="VIT model overview" class="paper-image">
    <figcaption class="image-caption">VIT model overview</figcaption>
</figure>