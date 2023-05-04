---
title: LeNet
date: 2023-05-04 20:14:30
tags:
---

### Model Structure
**Two convolutional layers + MLP**

Convolution, Activation and Pooling are a convolutional group.
Usually, when the height and width are halved, the number of channels is doubled.

### Code
```python
net = torch.nn.Sequential(
    Reshape(),

    nn.Conv2d(1,6,kernel_size=5,padding=2),
    nn.Sigmoid(),
    nn.AvgPool2d(kernel_size=2, stride=2),

    nn.Conv2d(6,16,kernel_size=5),
    nn.Sigmoid(),
    nn.AvgPool2d(kernel_size=2, stride=2),

    nn.Flatten(),

    nn.Linear(16*5*5,120),
    nn.Sigmoid(),

    nn.Linear(120,84),
    nn.Sigmoid(),

    nn.Linear(84,10)
)
```

### The Training Code by Muli
```python
def train_ch6(net,train_iter,test_iter,num_epochs,lr,device):
    def init_weights(m):
        if type(m) == nn.Linear or type(m) == nn.Conv2d:
            nn.init.xavier_uniform_(m.weight)
    net.apply(init_weights)
    print('training on',device)
    net.to(device)
    optimizer=torch.optim.SGD(net.parameters(),lr=lr)
    loss=nn.CrossEntropyLoss()
    animator=d2l.Animator(xlabel='epoch',xlim=[1,num_epochs],
                          legend=['train loss','train acc','test acc'])
    timer,num_batches =d2l.Timer(),len(train_iter)
    for epoch in range(num_epochs):
        metric=d2l.Accumulator(3)
        net.train()
        for i,(X,y) in enumerate(train_iter):
            timner.start()
            optimizer.zero_grad()
            X,y=X.to(device),y.to(device)
            y_hat=net(X)
            l=loss(y_hat,y)
            l.backward()
            optimizer.step()
            timer.stop()
            ...
```