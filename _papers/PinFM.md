---
layout: paper
title: "PinFM - Foundation Model for User Activity Sequences"
authors: []
year: 2025
journal: ""
paper: https://arxiv.org/pdf/2507.12704
---

## Summary

Authors propose a foundational model for sequential ranking which can be finetuned for various downstream tasks which require historical user sequence as input. The pretraining task is the usual next token prediction used in language modeling with slight modifications. Naive 20B foundational model is too slow to serve online traffic, so authors propose De-duplicated Cross Attention Transformer and INT4 quantized embeddings

## Key ideas

1. For pretraining, the model uses 2 years worth of user historical sequences
2. Heavily based on ID-based representations which the model can learn on its own.
3. For ID-based heavy input representations, we need a high number of samples for all items for the model to be able to learn its features. To handle cold start problems
    a. When finetuning, the candidate item embeddings are randomly initialized 10% of times. This simulates cold start problem.
    b. During finetuning, for fresh candidate items, authors use dropout to the output of the pretrained module. This kind of ensures that model should rely less on the output features when candidate item has low interaction.
4. Pretraining task is basically next token prediction. Specifically, given historical (item, action,timestamp) user sequence, we want to predict the next item in the sequence
    a. Naive next token prediction will be too compute heavy since total sequences are of the order of billions. To handle this, authors are only interested in predicting next items at timestamps which have a positive action associated in the near future.
    b. Its not exactly next token prediction. If a positive action item is found within L timestamps in the future, we include that target item embedding in the loss. Basically we want to predict embedding for any positive action item in the near future.
    c. Info-NCE contrastive loss is used where K negative embeddings are randomly chosen in-batch.
5. When integrating with ranking model, one key difference is availability of candidate item compared to pretraining time. The authors propose several ways, some of them using candidate item during sequence creation as transformer input and others with static user representation independent of candidate item. More complex way to input signal to transformer beats simpler ones.
6. Authors also propose two optimizations to make the architecture deployable
    a. Using INT4 embedding table to reduce storage and data transfer cost.
    b. Given that the user historical sequence changes very little compared to the candidate item (since we have to rank 100s to candidate given a user sequence), authors propose an optimization to prevent running attention over user sequence token >1 time

<figure class="image-container">
    <img src="{{ '/assets/images/pinfm.png' | relative_url }}" alt="Training & Finetuning of PinFM" class="paper-image">
    <figcaption class="image-caption">Training & Finetuning of PinFM</figcaption>
</figure>

## Limitations

1. The authors are not using event timestamp information at all. It can be a useful signal.
2. Selection of positive action to predict in the future seems like a difficult task. Table 4 results seem non-intutive.