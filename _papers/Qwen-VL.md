---
layout: paper
title: "Qwen-VL"
authors: []
year: 2023
journal: ""
paper: https://arxiv.org/pdf/2308.12966
---

## Summary

One of the first open source multi modal foundation models

## Key ideas

1. Uses Qwen-LM which is open source text only large model.
2. There is a separate vision encoder branch which uses pre-trained ViT based encoder. The input image is scaled to a fixed resolution before passing through the encoder. 
3. Image-text adapter: Similar idea as DETR, authors use a set of sparse learnable queries which cross attend to image features. These queries are passed through Qwen-VL and trained. This also ensures that visual features can be captured in fixed number of embeddings and the input image resolution can be changed. The paper uses 256 queries 
4. The main insight is that they worked hard to generate the data for model training. Training is performed in three phases
   1. Pre-training on weakly labeled web scraped text-image pairs. Qwen-LM is frozen in this phase. Total 1.4B samples for this stage and captioning task is used. Images are fed at 224x224 resolution
   2. Multi-task Pre-training on interleaved image/text data for other tasks likes grounding, OCR and referring etc. A total of 70M samples are used. The authors also increase the resolution to 448x448 to capture fine grained features for this task. The Image-text adapter ensures to always convert the visual feature to 256 fixed embeddings.
   3. Supervised-finetuning: Uses chat based data to give chat capabilities to the model (like chatGPT). ~350K samples at this point
