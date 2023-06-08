---
title: RCNN
date: 2023-06-08 10:11:24
tags:
---

### RoI pooling
Give us an anchor box,
It is evenly divided into n x m blocks. The calculated coordinates should be rounded.
The output is the maxmum value in each piece.

**No matter how big the anchor box is, it is always the size(n x m)**

**RCNN is to draw the anchor box first, and then extract the features of each anchor box.**

### Fast RCNN
**Use CNN to extract the features and then set the anchor box.**

### Faster RCNN
**Build a neural network to select the anchor box.**
This neural network is built to distinguish the quality of the anchor boxes.(a 2 classification problem)

### Mask RCNN
Change **RoI pooling** to **RoI align**.
RoI pooling leads to pixel-level offset. While RoI align solve the problem with linear interpolation.

Mask RCNN and Faster RCNN have the highest accuracy.