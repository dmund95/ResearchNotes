---
layout: paper
title: "InterFormer: Effective Heterogeneous Interaction Learning for Click-Through Rate Prediction"
authors: []
year: 2025
journal: ""
paper: https://arxiv.org/pdf/2411.09852
---

## Summary

The paper introduces a novel model architecture for effective interaction between sequential and non-sequential features. Authors present two-fold hypothesis of why current literature is not effectively mixing signals across the two feature modes. 
1. Unidirectional information flow: Current literature only uses information from one feature modality to another. 
2. Aggresive information aggregation: Current methods use techniques like max-pooling at early layers to aggregative sequence features which lead to a loss of information early on. 

This is based on the assumption that non-sequence features represent long term static "anchor personalities" about the user and item, whereas sequence features represent the dynamic short term user interests. Merging information across the two modalities should lead to maximum gains. For example, if a user who generally like electronics is navigating on headphone urls, the model should be able to selectively amplify signals for these features using bi-directional flow.

## Key ideas

1. Authors propose not to aggregate information aggresively using max-pooling layers and rather define learnable techniques which can selectively aggregate feature information.
2. They propose to enable bi-directional flow of information between sequence and non-sequence features. 
3. When passing information from one modality to the other, information is summarized to before merging with the other modality. In some way this is a sort aggregation to reduce noise when passing information.
4. Summarization in non-sequence modality is done via an MLP layer that transforms input feature of nxd to mxd where m &lt;&lt; n followed by a gating sigmoid function to scale features.
5. Summarization in sequence modality is done by concatenating three tensors: CLS token, learnable sparse queries PMA, latest K token embeddings. 
6. Interaction arch: This arch learns sequence aware non-sequence features. This is done simply by passing non-sequence features and summarized sequence features into an interaction module like wukong, DCN, DHEN. 
7. Sequence arch: This arch learns non-sequence aware sequence features. This is done by first scaling the sequence features by elementwise multiplying MLP transformed non-sequence features followed by a Multi-head attention module to learn temporal dependencies over sequence features. 

<figure class="image-container">
    <img src="{{ '/assets/images/interformer.png' | relative_url }}" alt="InterFormer architecture" class="paper-image">
    <figcaption class="image-caption">InterFormer architecture overview</figcaption>
</figure>

## Results

1. Authors run ablation experiments to show importance of bi-directional information flow, which beats all other permutations by a large margin. 
2. They also run ablation experiments to show the downside of doing information aggregation aggresively at early stages. 
3. Interformer is able to scale with longer sequences and more layers, showcasing scaling capabilities. 