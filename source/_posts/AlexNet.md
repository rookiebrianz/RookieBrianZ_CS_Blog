---
title: AlexNet
date: 2023-05-04 21:45:33
tags:
---

**a deeper and bigger LeNet**
Innovation: Dropout, Relu, Maxpooling

### model structure
net=nn.Sequential(
    nn.Conv2d(1,96,kernel_size=11,stride=4,padding=1),
    nn.ReLU(),
    nn.MaxPool2d(kernel_size=3,stride=2),

    nn.Conv2d(96,256,kernel_size=5,padding=2),
    nn.ReLU(),
    nn.MaxPool2d(kernel_size=3,stride=2),

    nn.Conv2d(256,384,kernel_size=3,padding=1),
    nn.ReLU(),

    nn.Conv2d(384,384,kernel_size=3,padding=1),
    nn.ReLU(),

    nn.Conv2d(384,256,kernel_size=3,padding=1),
    nn.ReLU(),

    nn.MaxPool2d(kernel_size=3,stride=2),
    
    nn.Flatten(),
    
    nn.Linear(6400,4096),
    nn.ReLU(),
    nn.dropout(p=0.5),


    nn.Linear(4096,4096),
    nn.ReLU(),
    nn.dropout(p=0.5),

    nn.Linear(4096,10)
)

### What if the model requires that the input size does not match the picture size?
Generally, the short side is resized to the corresponding size, and the long side is ignored first.
Then capture the picture, take out many pictures of the required size, and enter the model.


