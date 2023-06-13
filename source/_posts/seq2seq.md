---
title: seq2seq
date: 2023-06-13 22:16:24
tags:
---

The encoder is an RNN; The decoder is another RNN.
The final output of the encoder is input to the decoder.

- The real sentences were given during the training.
- Use the output of the previous moment when reasoning.

## BLEU: An evaluation method
The bigger the better.
n-gram: **Punishment for the short prediction; Long matching has the higher weight.**

## Beam Search
Seq2seq uses a greedy strategy, but greedy is not the best.
Beam Search: Save the best k candidates.
- k = 1 is greedy.
- k = n is not exhaustion.

## Attention Mechanism
Query: Random clues.
Key: Uncasual clues.(The previous ones were all random clues.)

In the seq2seq:
- The encoder outputs from each word as key and value.
- The output of the decoder to the previous word is query.

## Self-attention Mechanism
- Read the whole sentence at once.
- Self-attention does not record location information.
- Location code added to input data. (Add a little bit of detail so that the model can distinguish it; And sin or cos can give model the relative location information.)

Absolute location: Location coding matrix.

## Attention score
- Additive attention.
- Scale dot-product attention: The inner product of q and k divided by the root number d, which is insensitive to length.

The attention score is the similarity of q and k.
Attention weight is the result of the score softmax.

**Masked_softmax**
