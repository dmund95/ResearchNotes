---
layout: paper
title: "Qwen2-VL"
authors: []
year: 2024
journal: ""
paper: https://arxiv.org/pdf/2409.12191
---

## Summary

Foundation model for multimodal data: text, image, videos

## Key ideas

1. Unlike other foundation models that need to process images at fixed resolution, this model ingests images at any resolution.
2. To facilitate this, the authors come up with a new way to embed positional embeddings. All embeddings are now in 3 dimensions (time, height, width)
3. For videos the model might have to downsample it so as to limit the number of token to 16384
4. The model is able to understand videos over 20 mins long which is impressive

<figure class="image-container">
    <img src="{{ '/assets/images/qwen2-vl.png' | relative_url }}" alt="Multimodal rotary position embedding" class="paper-image">
    <figcaption class="image-caption">Multimodal rotary position embedding</figcaption>
</figure>

Overall nothing impressive. Seems very similar to other foundation models. Quite a lot of work is done getting huge amount of labeled data for various tasks like Visual question answering, image captions, and Agentic tasks. 