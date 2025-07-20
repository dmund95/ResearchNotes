---
layout: paper
title: "DINOv2"
authors: []
year: 2024
journal: ""
paper: https://arxiv.org/pdf/2304.07193
---

## Summary

The paper aims to learn foundational image features that can be used for downstream image based tasks.

## Key ideas

1. Uses ViT backbone to learn patch level features
2. For self supervised task
   1. It uses training techniques from DINO. Student model is aimed to learn same features as teacher model where teacher model uses exponential moving average of student params
   2. Masked patch level objective: generate same features for masked patch from student head as teacher head
3. One main task they did was to generate a clean dataset for training. Since open curated datasets are limited quantity, they parsed the internet to get 1.4B uncurated images. Then they use nearest neighbor search on embeddings to clean this 1.4B dataset and only choose those images which where similar to curated images. After this they have 142M images in total
4. For each downstream task, they use the learned features from this encoder and train task specific decoder. For example, for monocular depth, they use DensePredictionTransformer head. 