---
title: Transfer convolution
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
- Input: 
height=n
width=n
kernel=k
padding=p
stride=s
- Output:
n'=sn+j-2p-s

**If we want to double the height and width, k=2p+s.**