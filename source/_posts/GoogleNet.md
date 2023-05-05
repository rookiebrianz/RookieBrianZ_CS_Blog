---
title: GoogleNet
date: 2023-05-05 10:56:45
tags:
---
### Inception Block
Don't change the width and height, only change the number of channels.
Four paths extract information from different levels, and then merge it in the output channel dimension.

1. Path 1: 1x1 Conv
2. Path 2: 3x3 Conv + 1x1 Conv
3. Path 3: 5x5 Conv + 1x1 Conv
4. Path 4: 1x1 Conv + 3x3 MaxPool

The outputs of 4 paths will be stacked by the code named **concat**. Stacked on the channels.

### Subsequent variants
- Inception-BN: batch normalization.
- Inception-V3: replace 5x5 Conv with many 3x3 Conv; replace 5x5 Conv with 1x7 and 7x1 Conv; replace 3x3 Conv with 1x3 and 3x1 Conv.
- Inception-V4: Residual connection.