---
title: RNN
date: 2023-06-13 21:04:45
tags:
---

**x_t is related to h_t + x_(t-1)**: x is input, h is hidden variable, o is output.

x_(t-1) -> h_t;
h_t -> o_t;
loss: o_t, x_t;

**h_t = (W_hh * h_(t-1) + W_hx * X_(t-1) +b_h)**
If without W_hh * h_(t-1), it will degenerates into MLP.

W_hh saves the timing information.

**NLP doesn't use cross entropy, however, use confusion perplexity (exp(cross entropy)).**
The value of confusion perplexity is much bigger. It is easier for the model to see the little improvement.
Confusion perplexity 1 means perfect, infinity is the worst case.


**Gradient tailoring**
It can prevent gradient explosions.
If the gradient g exceeds theta, then drag it back to theta.
**g <- min（1，theta/||g||）g**