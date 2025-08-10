---
layout: paper
title: "LLaVa"
authors: []
year: 2023
journal: ""
paper: https://arxiv.org/pdf/2304.08485
---

## Summary

This paper introduces a general purpose visual assistant model that can ingest both images + text to converse with humans

## Key ideas

1. The novelty of this paper is how they create multimodal instruction-following dataset to train this model. They parse internet for (image, caption) pairs first. To generate questions for instruction tuning, they leverage GPT-4. The authors categorize questions in 3 forms; conversational, description and complex reasoning. Since GPT-4 is text only, we use different prompt for each of these categories to get GPT-4 to ask questions as well as answer those questions by itself. So this is a combination of clever prompt engineering and leveraging text only model. 
2. Once we have such dataset, it can be basically considered as a sequence of token (image, question,answer, question, answer) which can be trained by the general LLM auto-regressive loss
3. CLIP image encoder is used and Vicuna text encoder is used. To align the visual features to text feature space, linear projection layer is learnt to transform image embedding.

<figure class="image-container">
    <img src="{{ '/assets/images/llava.png' | relative_url }}" alt="LLaVa model architecture" class="paper-image">
    <figcaption class="image-caption">LLaVa model architecture</figcaption>
</figure>

## Limitation

1. The model can not handle interleaved images + text information. 
2. Each conversation can only have upto single image with all questions pertaining to that image. 