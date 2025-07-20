---
layout: paper
title: "CLIPSeg"
authors: []
year: 2022
journal: ""
paper: https://arxiv.org/pdf/2112.10003
---

## Summary

The paper tackles referring segmentation task for 2D images. It can handle unseen classes due to using CLIP based encoders. This is useful since adding new classes to DL models requires retraining which is costly.
To condition desired image, the model supports either text or image based prompt (visual conditioning)

## Key ideas

1. Uses frozen visual / text encoder from CLIP. ViT/16 architecture. Adds minimal trainable decoder transformer layers on top for segmentation task. Feature resolution stays same across the layers since its a ViT
2. PhraseCut dataset is used to train the model. The dataset contains 340K (text,image) -> segmentation mask samples. 
3. Inspired from UNet architecture, the model uses skip connections from different layers in encoder. Number of decoder layers == number of skip connection routes. 
4. For text based conditioning, we choose the last layer features and do an affine transformation using learnable scale and shift conditioned on text embedding. This tells the model to excite the features in patches which are related to the text. Alpha(t) * feature_map + beta(t)
5. Visual prompting is a little more complicated. The authors figured out the best way to condition segmentation based on images after trying various strategies of cropping / zooming / background_blurring

## Evaluation

1. The results section seem a bit weak overall. For classes seen in during training, there are models which perform segmentation far better than CLIPSeg.
2. Looks like the paper's strong point is that it has better performance on unseen classes due to its inherent ability to understand text because of CLIP pretraining. 