---
title: ResNet
date: 2023-05-05 12:15:58
tags:
---

### Residual Model
**f(x)=x+g(x)**
The result will not get worse.
If g(x) deteriorates or has little effect, the gradient of it will be relatively small and will not be updated much.

**Two kinds of blocks**
1. The height and width are halved.(Usually, the number of channels is doubled by the use of 1x1 Conv)
2. The height and width are not halved.

**Different ResNet**
**ResNet34 is commonly used. The next is ResNet50.**
ResNet101 and ResNet152 are usually used to take part in competition.

### How can ResNet train to the 1000th floor without gradient disappearing?
**change multiplication to addition**
- y=f(x)
gradient = ∂y/∂w
update weight: w = w - (lr*gradient)
- y'=g(f(x))
gradient = ∂y'/∂w = ∂y'/∂y * ∂y/∂w = ∂g(y)/∂y * ∂y/∂w
- y"=f(x)+g(f(x))
gradient = ∂y"/∂w = ∂y/∂w + ∂y'/∂w

Avoid the disappearance of the gradient;
The layer close to the data can get a large gradient, and then update it.
