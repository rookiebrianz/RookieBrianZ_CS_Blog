---
title: VGG
date: 2023-05-04 22:07:40
tags:
---

**a deeper and larger network than AlexNet**
Combine the convolutional layer into blocks.
VGG is made by 3x3 convolutional layers stacking.

- LeNet: (2 convolutional layers + pooling layers) + 2 FC layers 
- AlexNet: ReLU, Dropout, MaxPooling
- VGG: VGG blocks

**A website recording the different models: https://cv.gluon.ai/model_zoo/classification.html**

Use repeatable blocks to build a convolutional neural network.

**VGG_Block**
```python
def vgg_block(num_convs, in_channels, out_channels):
    layers = []
    for _ in range(num_convs):
        layers.append(nn.Conv2d(in_channels, out_channels, kernel_size=3, padding=1))
        layers.append(nn.ReLu())
        in_channels=out_channels
        layers.append(nn.MaxPool2d(kernel_size=2， stride=2))
        return nn.Sequential(*layers)
```

**VGG**
```python
def vgg(conv_arch):
    conv_blks = []
    in_channels=1
    for (num_convs, out_channels) in conv_arch:
        conv_blks.append(vgg_block(
            num_convs, in_channels, out_channels))
            in_channels = out_channels

    return nn.Sequential(
        *conv_blks, nn.Flatten(),
        nn.Linear(out_channels * 7 * 7， 4096), nn.ReLU(),
        nn.Dropout(0.5), nn.Linear(4096，4096), nn.ReLU(),
        nn.Dropout(0.5), nn.Linear(4096，10))

net = vgg(conv_arch)
```
