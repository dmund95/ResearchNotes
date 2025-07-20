---
layout: paper
title: "LLaMa Adapter"
authors: []
year: 2024
journal: ""
paper: https://arxiv.org/pdf/2303.16199
---

## Summary

It's a form of parameter efficient finetuning technique. The idea is to take a pretrained LLM (LLaMa in this paper) and finetune it for downstream task (instruction tuning in this paper). Authors propose to freeze LLM modules and are able to finetune a model within 1 hour with comparable performance to fully finetuned models.

## Key ideas

1. We keep the LLM layers frozen for efficient finetuning. To finetune for specific task, the idea is to introduce task specific "prompt embeddings". Think of these as abstract learnable embeddings that contain information about how the embeddings in LLM should interpret the task. 
2. These special prompt embeddings are introduced at the last L layers of the LLM. Apart from the usual token embeddings, next token prediction attends to the previous tokens as well as these special prompt embeddings.
3. Since prompt embeddings are initialized randomly, gated attention is used similar to ideas from Flamingo and ControlNet. Idea is to inject a learnable tanh layer that initializes with zero (so that LLM attention layer does not attend to these prompt embeddings initially) 
4. Simply put, the attention affinity matrix is divided into two parts, one with next token embedding attending to the previous tokens (usual LLM) and one attending to all newly introduced prompt embeddings. Softmax is taken over the two matrices independently to compute the final value feature for next token prediction. Softmax matrix over prompt embeddings is modulated by tanh gated logic. 
5. Multi modal reasoning: The technique can also be used to condition on images. The idea is to use CLIP image encoder to get image embeddings and add these image features to the prompt embeddings to generate image conditioned prompt embeddings. These embeddings are then passed through the zero gated attention layers explained above. 