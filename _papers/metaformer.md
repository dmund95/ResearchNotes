---
layout: paper
title: "MetaFormer"
authors: []
year: 2022
journal: ""
paper: https://arxiv.org/pdf/2111.11418
---

## Summary

TokenMixer module is responsible for mixing token information in a transformer architecture. Usually this TokenMixer module is implemented as a self-attention block. Recently spatial MLPs were introduced as TokenMixer.

This paper uses a very simple average pooling operation as the TokenMixer module. Idea is to pool nearby token features in K-sized sliding window.

For some reason this simple token mixing strategy performs very competitively with attention based architecture. 