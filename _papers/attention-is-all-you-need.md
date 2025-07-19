---
layout: paper
title: "Attention Is All You Need"
authors: ["Ashish Vaswani", "Noam Shazeer", "Niki Parmar", "Jakob Uszkoreit", "Llion Jones", "Aidan N. Gomez", "Lukasz Kaiser", "Illia Polosukhin"]
year: 2017
journal: "NIPS 2017"
doi: "10.48550/arXiv.1706.03762"
topic: "machine-learning"
tags: ["transformers", "attention", "neural-networks", "nlp"]
key_points:
  - "Introduces the Transformer architecture based solely on attention mechanisms"
  - "Eliminates the need for recurrence and convolutions in sequence modeling"
  - "Achieves state-of-the-art performance on machine translation tasks"
  - "Enables better parallelization during training"
methodology: "The authors propose a novel architecture that relies entirely on attention mechanisms to draw global dependencies between input and output. The model uses multi-head self-attention and position encodings to process sequences."
conclusions: "The Transformer model demonstrates that attention mechanisms alone are sufficient for achieving excellent performance on sequence transduction tasks, while being more parallelizable and requiring significantly less time to train."
---

## Summary

This groundbreaking paper introduces the Transformer architecture, which has become the foundation for most modern NLP models. The key innovation is the use of self-attention mechanisms that allow the model to relate different positions of a single sequence to compute a representation of the sequence.

## Architecture Details

<div class="image-container">
  <img src="https://via.placeholder.com/500x600/3498db/ffffff?text=Transformer+Architecture" 
       alt="Transformer Architecture" 
       class="paper-image">
  <p class="image-caption">Figure 1: The Transformer model architecture</p>
</div>

### Multi-Head Attention
The model uses multiple attention heads to focus on different representation subspaces:
- **Scaled Dot-Product Attention**: Computes attention weights using query, key, and value vectors
- **Multi-Head**: Uses multiple attention heads in parallel
- **Self-Attention**: Applied to relate different positions within the same sequence

### Position Encoding
Since the model contains no recurrence or convolution, positional encodings are added to input embeddings to give the model information about position.

### Encoder-Decoder Structure
- **Encoder**: 6 identical layers with multi-head self-attention and position-wise feed-forward networks
- **Decoder**: 6 identical layers with masked multi-head attention to prevent positions from attending to subsequent positions

## Impact

This paper has had tremendous impact on the field:
1. **BERT** and other bidirectional models
2. **GPT** series and autoregressive language models
3. **T5** and text-to-text transfer transformers
4. **Vision Transformers** extending the architecture to computer vision

## Key Equations

The attention function can be described as:
```
Attention(Q, K, V) = softmax(QK^T / √d_k)V
```

Where Q, K, V are the query, key, and value matrices respectively.

## Personal Notes

The simplicity and effectiveness of the attention mechanism is remarkable. The ability to capture long-range dependencies without the sequential nature of RNNs was a major breakthrough. The parallelizability also makes training much more efficient. 