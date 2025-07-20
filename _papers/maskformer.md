---
layout: paper
title: "MaskFormer"
authors: []
year: 2021
journal: ""
paper: https://arxiv.org/pdf/2107.06278
---

## Summary

The paper proposes a method to unify semantic segmentation and instance segmentation. Semantic segmentation was modeled as per pixel classification task while instance segmentation was modeled as mask classification task. The authors claim that mask classification is enough to model both tasks. The idea is heavily inspired from DETR architecture. Unlike Mask-RCNN or DETR which first compute the bounding boxes, MaskFormer bypass the need

## Key ideas

1. MaskFormer predicts N binary masks (representing N=100 instances) and each mask corresponds to one of K classes (K+1 to account for NONE class)
2. Given N_gt < N ground truth masks and the associated instance class id, Hungarian matching is used  to find optimal matching. The matching function is sum of class cross entropy loss + binary mask loss
3. Given the optimal matching, loss function is a sum of class cross entropy + binary mask loss (focal loss + dice loss)
4. Uses Swin Transformer image encoder which generates feature map with 32 stride. This feature map is passed through pixel decoder (just FPN module) to upsample. Just like DETR, N learnable abstract queries attend to the encoded features. These queries contain global semantic information. To predict classes for masks, these query embeddings are passed through MLP -> softmax layer. To predict binary masks, pixel-wise dot product is taken with the output of pixel decoder. 