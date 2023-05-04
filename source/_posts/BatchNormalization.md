---
title: Batch Normalization
date: 2023-05-03 20:17:35
tags:
---

**BN layer can accelerate convergence without changing the accuracy of the model.**
This method has a better effect on **deep networks** than shallow networks.
Due to the reverse derivation, the gradient near the output is relatively large, the gradient near the input is relatively small. Therefore, the update speed near the output position is fast, the update speed near the data position is slow.

**How to solve this problem?**
Fix the distribution (mean, variance)

#### Theory:
**(Input-Mean)/sqrt(Variance) * Gamma + Beta**
Among them, gamma and beta can be learned by the network.
- When doing inference, use the global mean and variance.
- When training, use the current mean and variance.
**mean = current global mean * 0.9 + ( 1.0 - 0.9 ) * current mean**

BatchNormalization is **a linear transformation**, which acts on the **output of the full connection layer and the convolutional layer**, **in front of the activation function**. Or act on the input of the FC layer and the convolutional layer.

- For the full connection layer, BN acts on the characteristic dimension.
- For the convolutional layer, BN acts in the channel of dimension.

#### Purpose:
Author: reduce the transfer of internal covaribles.
The subsequent: add noise to each small batch. The mean value is random offset, the standard deviation is random scaling.

#### Code:
nn.batchnorm2d()

