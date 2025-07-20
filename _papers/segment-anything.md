---
layout: paper
title: "Segment Anything"
authors: []
year: 2023
journal: ""
paper: https://arxiv.org/pdf/2304.02643
---

Foundational model for Segmentation !! 

## Summary

The paper redefines segmentation as a promptable task. The query can be of 4 types
1. Point 
2. Box
3. Mask
4. Text

By supporting these types of query to get segmentation, the authors claim this can be used downstream in a closed loop system easily (for example in addition to object detection task)

## Key ideas

1. Two main contributions
   1. Promptable segmentation model
   2. Model in the loop data annotation engine: Segmentation masks are iteratively refined with human experts to generate 1B masks over 11M images
2. Three main components in the model
   1. Image encoder: Pretrained ViT using MaskAutoEncoder objective. The output feature map is 1/16 of original image
   2. Prompt encoder: Different modalities are encoder separately
      1. Text: CLIP based encoder to encode text 
      2. Point: The point embedding is basically sum of position embedding of physical point + learned point embedding 
      3. Box: 
   3. Mask decoder: Various attention modules to attend features across image + prompt embeddings 