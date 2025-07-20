---
layout: paper
title: "Qwen-VL: A Versatile Vision-Language Model for Understanding, Localization, Text Reading, and Beyond"
authors: ["Alibaba Group"]
year: 2023
journal: "CVPR"
---

## Summary

One of the first open source multi modal foundation models for VLM !!

## Key Innovations

There is a separate vision encoder branch which uses pre-trained ViT based encoder. The input image is scaled to a fixed resolution before passing through the encoder. 

### Pre-training Objectives

1. **Masked Language Model**: 15% of tokens are masked, with 80% replaced by [MASK], 10% by random tokens, and 10% unchanged
2. **Next Sentence Prediction**: Binary classification to understand sentence relationships

## Architecture

- Based on the Transformer encoder
- Two model sizes: BERT-Base (12 layers) and BERT-Large (24 layers)
- Uses WordPiece tokenization with 30,000 vocabulary
- Maximum sequence length of 512 tokens

<div class="image-container">
  <img src="{{ '/assets/images/bert/bert-architecture.png' | relative_url }}" 
       alt="BERT Architecture" 
       class="paper-image">
  <p class="image-caption">Figure 2: BERT bidirectional training approach</p>
</div>

## Personal Insights

The masked language modeling approach was brilliant - it allows the model to see context from both directions while still maintaining a reasonable pre-training objective. The fine-tuning approach also made BERT very practical for real-world applications. 