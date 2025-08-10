---
layout: paper
title: "Flamingo"
authors: []
year: 2022
journal: ""
paper: https://arxiv.org/pdf/2204.14198
---

## Summary

This is a foundation model that can take as input interleaved image / video + text and outputs text only.

## Key ideas

1. The paper makes use of pretrained LLM which is kept frozen.
2. One of the key ideas is to inject visual information from images/video by adding extra attention layers in between the attention layers of LLMs. Its ensured that initially the output from this new visual-text attention layer is zero so that in the beginning features are similar as text only features from LLM. This is to stabilize training initially. Similar idea is there in ControlNet.
3. The new attention layers use masked attention matrices. Each text token only attends to just previous image tokens, rather than attending to all the image tokens before it. This makes sense because of the nature of how prompts are generated at training / inference time. Its assumed that each sentence is describing the last image only. 
4. To generate visual token, the authors train image encoder and freeze it. The image encoder is trained using contrastive learning. Authors train a separate stronger backbone based image encoder compared to CLIP and show it gives better performance.
5. Since the image resolutions can be varied, authors use similar idea as DETR to generate fixed number of embeddings (64) to describe the visual context. Basically there are 64 learnable queries that attend to visual tokens and aggregate features from. 
6. Surprisingly, training the LM layers lead to performance drop compared to freezing them. Paper claims this is because of catastrophic forgetting. However given the scale of the training data ~2B samples in total, not sure how this is justified. 

<figure class="image-container">
    <img src="{{ '/assets/images/flamingo1.png' | relative_url }}" alt="Flamingo architecture overview" class="paper-image">
    <figcaption class="image-caption">Flamingo architecture overview</figcaption>
</figure>

<figure class="image-container">
    <img src="{{ '/assets/images/flamingo2.png' | relative_url }}" alt="Gated attention layers" class="paper-image">
    <figcaption class="image-caption">Gated attention layers</figcaption>
</figure>