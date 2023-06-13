---
title: Bert
date: 2023-06-13 23:46:37
tags:
---

The encoder of Transformer.
- The bigger model.
- The input is pairs of sentences.
- Use two tasks during training.

Base：blocks=12 hidden=768 heads=12 parameters=110M
Large：blocks=24 hidden=1024 heads=16 parameters=340M

**The difference between Bert and Transformer**
Modification of input: 
- Each sample is a pair of sentences.
- Use Segment embedding to divided sentences.
- Let the model learn position embedding by itself.

**Two tasks**
1. Language model with mask
Replace any word with mask with a certain probability.

2. Prediction of the next sentence.
50% probability of choosing adjacent sentence pairs.
50% probability to choose random sentence pairs.

## Bert fine-tuning
Bert + FC layer
- **Sentence classification**, just take the vector of cls to the classifier.
- **Named entity recognition**, non-special word elements put into the full connection layer classifier
- **Question answering**

