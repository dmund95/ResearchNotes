---
layout: paper
title: "Florence"
authors: []
year: 2021
journal: ""
paper: https://arxiv.org/pdf/2111.11432
---

## Summary

The paper introduces a foundation model that can be adapted to various downstream tasks like object detection, VQA, Captioning, video action recognition

## Key ideas

1. The pretraining strategy is the same as ALIGN paper (which is very similar to CLIP). The difference from contrastive learning proposed in CLIP is that CLIP assumes a single positive pair in one batch. However the authors propose that web scale data can have multiple images with similar text so there might be multiple positive pairs in the data. Hence contrastive loss will can have multiple positive pairs in a batch depending on label assigned to (image, text) pair. The labels are assigned using hashing over text. A total of 350M image-text dataset is created for pretraining.
2. Swin architecture is used for image encoder. 
3. Object detection requires finer feature representation. To aid this, the authors use an object detection dataset containing 9M samples. To learn finer features from the pretrained Swin encoder, feature maps from different scales in the feature pyramid network are chosen and inter-channel (Squeeze & excitation network) / intra-channel attention operations are performed to come up with object level feature representation
4. For VQA, the pretrained Swin encoder after object detection task is used as image encoder. For text, pretrained RobertA model is used. To share information across modalities, co-attention module is used. Its basically self-attention followed by cross-attention blocks. 
5. For Video understanding, learnt 2D conv weights are copied over to 3D conv weights. This 3D conv layer is used for temporal image features. 
6. Zero shot classification: A set of all text class names are used as query and for input image, we find the most similar text embedding 
7. Fine-tune classification: A linear layer on top of frozen image encoder is trained for the task
8. Zero shot object detection: Follows idea from R-CNN. Proposal bounding boxes are predicted via training for class agnostic detector head. This is only responsible to predict foreground bounding boxes. The proposal boxes are then passed through zero-shot classification task as described above. 