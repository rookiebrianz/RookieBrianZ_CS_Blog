---
title: NiN
date: 2023-05-05 10:28:47
tags:
---

- Number of convolutional layer parameters: **input channels x output channels x windows height x windows width**
- Number of FC layer parameters: **input channels x feature map height x feature map width x digits of output**

### NiN Block
1x1 Convolution
1x1 Convolution
Convolution

### Innovation of NiN
1. No FC layer.
2. Take turns to use the NiN block and the maxpooling layer with the stride of 2.
3. Finally, use the global average pooling layer to get the output.

**Advantages:** Global average pooling layer replaces the FC layer. **The amount of calculation is reduced.**
**Drawbacks:** Convergence slows down. (Difficult to fit data)

### model structure
- Output
- SoftMax
- Global AvgPool
- NiN Block(3x3 pad=1)
- MaxPool(3x3 stride=2)
- NiN Block(3x3 pad=1)
- MaxPool(3x3 stride=2)
- NiN Block(5x5 pad=1)
- MaxPool(3x3 stride=2)
- NiN Block(11x11 stride=4)
