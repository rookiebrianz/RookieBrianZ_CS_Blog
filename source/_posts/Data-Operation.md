---
title: Data Operation
date: 2023-04-19 09:18:15
tags:
---

### Data Access

**Whether it is Numpy or Torch, the array subscript starts from 0.**

- If you want to access a certain line, such as the first line, you can use [1, :].
- What does [1:3, 1:] mean? It means, from the row it is to access the first and second row, from the column, it is to access after the first column.
- What about [::3, ::2] ? It means accessing the data, one interval every 3 rows and every 2 columns. 
- The shape of tensor([[[2,1,4,3],[1,2,3,4],[4,3,2,1]]]) is (1,3,4)
#### Common coding operations
```python
torch.arrange(12) #create a vector from 1 to 11
x.shape #the shape of x
x.numel() #the number of elemets
x.reshape(3,4) #'reshape(1,3,4)' is also allowed; It is continuous in the row.
torch.zeros((2,3,4)) or torch.ones((2,3,4)) #create a tensor which shape is (2,3,4)
tensor([[2,1,4,3,],[1,2,3,4],[4,3,2,1]]) #list of list

```