---
title: SSD
date: 2023-06-12 22:08:47
tags:
---

**The accuracy is much lower than that of the rcnn series.**

- A basic network to extract features.
- Several convolutional layers to halve the height and width.
- The model will generate an anchor box every layer. 
(The bottom box fits small objects, the top section fits large objects.)

**Predict the category and edge box for each anchor box.**

