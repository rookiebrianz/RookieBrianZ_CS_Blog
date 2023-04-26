---
title: GPU
date: 2023-04-26 17:23:26
tags:
---

**!nvidia-smi**
We can use this code to check the GPU. If the GPU occupancy rate is not high, it means that the model is not very good.
- torch.device('cpu')
- torch.cuda.device('cuda')
- torch.cuda.device('cuda:1')
We can use the code just like: **torch.randn((2,3), device=torch.device('cuda:1'))**

**torch.cuda.device_count()**
Show how many GPUs you have.

**Common Used Function**
If you only have one GPU:
```python
def try_gpu(i=0):
    if torch.cuda.device_count() >= i + 1:
        return torch.device(f'cuda:{i}')
    return torch.device('cpu')
```

If you have more GPUs than one:
```python
def try_all_gpus():
    devices=[
        torch.device(f'cuda:{i}') for i in range(torch.cuda.device_count())]
    return devices if devices else [torch.device('cpu')]
```

**x.device**
We could check whether the parameters are in the CPU or GPU.
When creating the tensor, we could create it in the GPU directly.
```python
x=torch.ones(2,3,device=try_gpu())
```
**Tensor X and tensor y must be in the same GPU to add or subtract operations.**

**net.to(device=try_gpu())**
move the module to GPU. module only can be moved by the code 'to(device)'.
And, we could make sure that the tensor is in GPUs through the code: **net[0].weight.data.device**


