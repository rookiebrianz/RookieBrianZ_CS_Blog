---
title: Sequence Model
date: 2023-06-13 20:54:38
tags:
---

**Markov Hypothesis: Assume that the current data is only related to t past data points.**

**Latent variable model:**
- Summarize historical information with latent variables.
- Latent variables + x -> new latent variable
- New latent variable + x -> new x

Text pre-processing(Chinese): jieba 

Language model: bert, gpt3

**If the input is very long, we usually use Markov hypothesis.**