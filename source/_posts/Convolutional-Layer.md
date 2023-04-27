---
title: Convolutional Layer
date: 2023-04-27 14:28:21
tags:
---
The convolutional layer is obtained by using **translation invariance** and **locality** for the full connection layer.

### nn.Conv2d
The input data requirements of this function is 4D. (batch_size, channels, width, height).
**conv2d=nn.Conv2d(input,output,kernel_size,padding,stride)**
Computational complexity: O(c_i * c_o * k_h * k_w * m_h * m_w)


### padding
Usually, the value of padding is **kernel-1**. In this way, the shape of output is the same as the input.

**Why is the convolutional kernel usually set to odd number?**
Because we want the padding is symmetric.

### stride
**How to caculate the shape of output?**
(n-k+p+s)/s

**We could control rows and columns separately.**
conv2d=nn.Conv2d(1,1,kernel_size=(3,5),padding=(0,1),stride=(3,4))

### 1x1 kernel
1x1 convolutional layer can be ragarded as Fc layer.
Comes from: <https://sebastianraschka.com/faq/docs/fc-to-conv.html>

My understanding: the channel of input is 4. The output channel is 2. Of course, we could use 1x1 convolutional layer to do this. But, we can also regard this operation as a combination FC layer, the input is 4, the output is 2.