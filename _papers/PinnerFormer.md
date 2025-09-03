---
layout: paper
title: "PinnerFormer: Sequence Modeling for User Representation at Pinterest"
authors: []
year: 2022
journal: ""
paper: https://arxiv.org/pdf/2205.04507
---

## Summary

The paper proposes sequential model to learn single user embedding that captures long term interests. This is an upstream model whose inference is run daily and the user embedding is passed to the v0 (head) models. To circumvent the issues of large training compute and complex streaming infrastructure associated with realtime inference, the authors chose daily batch inference to update user embeddings. Loss function is slightly tweaked from naive next token prediction. 


## Key ideas

1. Given a sequence of historical (post, action) a user has engaged with, we want to recommend possible positive engaging posts. The paper uses transformer decoder-only architecture where post embeddings are coming from PinnerSage model (CU + interaction information) which is a graph model at Pinterest. The output embedding at the last timestamp is called the user embedding. This learnt output user embedding lies in the same vector space as post embeddings and this ensures we can use inner product as a measure of similarity.

2. To capture long term interest and ensure model is less sensitive to freshness, authors propose all action loss which aims to predict all positive engagements within K timestamps in the future. Ablation experiments show that this "dense all action loss" significantly helps the model decrease gap in performance when inferred realtime vs daily. 


<figure class="image-container">
    <img src="{{ '/assets/images/Pinnerformer1.png' | relative_url }}" alt="Training objectives" class="paper-image">
    <figcaption class="image-caption">Training objectives</figcaption>
</figure>

3. Loss: Authors use InfoNCE loss with negatives mixed from 2 places.
    a. In-batch negatives: Positive engaged post for other user sequences 
    b. Random negative sampling: Random posts from data. 

<figure class="image-container">
    <img src="{{ '/assets/images/Pinnerformer2.png' | relative_url }}" alt="Contrastive loss" class="paper-image">
    <figcaption class="image-caption">Contrastive loss</figcaption>
</figure>

4. Instead of learning user representation for each type of action (Repins, Closeups, and Clicks), the authors claim that single unified user embedding is more scalable. However, this obviously comes at a performance cost, the diversity in the retrived candidate posts will be reduced compared to if we had multiple user embeddings learnt. 

5. Offline eval metrics: This is a representation learning problem. Authors propose the following metrics to evaluate the model against PinnerSage baseline. 
    a. Recall@k
    b. Diversity in retrieved posts for a user
    c. Global diversity in retrieved posts across all users

## Limitations
