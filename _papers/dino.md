---
layout: paper
title: "DINO"
authors: []
year: 2021
journal: ""
paper: https://arxiv.org/pdf/2104.14294
---

DINO => self-distillation with no labels

## Summary

The paper introduces a self supervised learning method for images. Idea is to train on images with no associated labels and learn features that are useful for downstream tasks.

## Key ideas

1. Introduces knowledge distillation based self supervised learning approach. The technique can work with either ViT or CNN based architecture.
2. Student and teacher model are initialized with same parameters / architecture
3. For a given image, we generate several local views (by cropping, rotating) and 2 global views of the image. Local views contain < 50% of image pixel whereas global views contain > 50%
4. Global views are passed through the teacher model and local views are passed through the student network. A probability distribution over K-dimensions is computed using softmax with temperature parameter. Student network's loss function is cross entropy loss so as to mimic teacher feature vector. 
5. Teacher network weights are updated using exponential moving averages from student teacher weights. 
6. Intuitively, student network is learning to generate global features from local image views. 
7. There is a possible mode collapse problem here, if both the models just output K dimensional one hot vector. To avoid this, we track the average output feature vector from teacher model and subtract this baseline while computing softmax. 

This is not a foundational model because the dataset scale is very limited. DINOv2 builds on top of this approach to train larger model on larger dataset 