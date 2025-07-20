---
layout: paper
title: "DETR"
authors: []
year: 2020
journal: ""
paper: https://arxiv.org/pdf/2005.12872
---

## Summary

Introduces sparse query based detection 

Input image passed through CNN. Flatten + positional encoding

Passes through the transformer encoder. Learnable queries used in decoder with values and keys from encoder to predict class id and bbox dimensions per query 

Find optimal matching between query predictions and GT using L_match (sum of classification loss + regression loss)
Use optimal matching to compute the final loss and backprop 