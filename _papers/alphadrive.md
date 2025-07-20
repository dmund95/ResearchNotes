---
layout: paper
title: "AlphaDrive"
authors: []
year: 2025
journal: ""
paper: https://arxiv.org/pdf/2503.07608
---

## Summary

Aim is to predict high level trajectory actions given raw camera videos. This is similar to other papers where another end to end planner module is used to generate high frequency control output given this low frequency high level planning strategy.

## Key ideas

1. Takes inspiration from Deepseek and incorporates RL training in high level trajectory planning task using VLMs.
2. The model takes raw sensor data as input and outputs high level trajectory planning. 
3. Dataset is limited; 120K videos of 3 second each and the corresponding planning annotation like "take left, slow down"
4. They use supervised fine tuning on pretrained QWen-2B VLM to inject reasoning capabilities into the model. They do this using a larger model (GPT-4o) to generate reasoning behind planning decision. They fine-tune QWen using this dataset as warm up.
5. The model is then asked to generate different outputs containing both reasoning & planned trajectory, given a sequence of frames. Each output is assigned some reward based on heuristics and trained with GRPO algorithm. 

## Results

1. RL based model is able to generate diverse output trajectories which are correct. The authors attribute this to the emergent intelligence behaviour due to RL
2. In limited data paradigm, SFT performance is lacking and RL impact is much higher. 