---
title: Transposed Convolution
date: 2023-06-12 22:39:41
tags:
---

The shape is inverse, while the value is not, so **it is not a deconvolution**.

- padding is 0, stride is 1.
- padding is p, stride is s.
1.Insert s-1 rows or columns between rows and columns.
2.Border padding k-p-1.
3.Flip the kernel matrix.
4.Do normal convolution.

**Shape conversion**
- **Input:**
height=n
width=n
kernel=k
padding=p
stride=s
- **Output:**
n'=sn+j-2p-s

**If we want to double the height and width, k=2p+s.**

### Fully Connected Neural Network(FCN)
Input Picture -> cnn -> 1x1 conv -> Transposed conv -> Output picture

The size of output picture is k x 224 x 224. (k is the number of types.)

**Code:**
net=nn.Sequential(*list(pretrained_net.children())[:-2])
(Delete the last two layers.)

**Initialize the transposed convolution layer with bilinear interpolation upsampling. For the convolution layer, we use xavier initialization parameters.**