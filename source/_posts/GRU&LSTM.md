---
title: GRU & LSTM & Others
date: 2023-06-13 22:07:53
tags:
---

## GRU
Update Gate + Reset Gate (W)
X * W + H * W + b

## LSTM
The performance is similar to that of GRU.
Forget Gate + Input Gate + Output Gate

## Two-side RNN
**RNN only looks at the past, but we can also look at the future.**
- Forward hidden layer output results.
- Backward hiiden layer re-enter the result above.
**Take the two result above as H.**

It is usually used to extract features and fill in the blanks of the sequence, rather than predicting the future.
