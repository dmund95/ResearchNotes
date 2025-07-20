---
layout: paper
title: "Mask2Former"
authors: []
year: 2022
journal: ""
paper: https://arxiv.org/pdf/2112.01527
---

## Summary

Closely builds on top of MaskFormer architecture with 3 main changes

1. High resolution feature attention: In MaskFormer, abstract queries attend to only the last feature map from image encoder. In Mask2Former, abstract queries are refined over various blocks with each block attending to a different resolution of the feature map from the pixel decoder. 
2. Masked attention in transformer decoder: Decoder uses attention to refine abstract queries over sequential blocks. Since there are high resolution feature maps for queries to attend over, authors propose masked attention. The idea is that each query attends to the relevant pixels only instead of attending over all pixels. This also helps the model converge faster, since slow convergence in transformer architecture is due to global attention
   1. Where does the mask come from ? Like Denoising-DETR, there is a loss at each decoder layer. Mask is learnt based on interaction of query with feature values dot product. It  is of shape N x HW which is thresholded at 0.5. So its a map of 0/1 binary values. 
3. Decoder layer attention module swap: Instead of self attention -> cross attention -> FFN the authors use masked cross_attn -> self_attn -> FFN 
4. Instead of calculating masked loss on all pixels, K random points are chosen to compute mask loss. This increases training efficiency 