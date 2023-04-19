---
title: Data Operation
date: 2023-04-19 09:18:15
tags:
---

### Data Access

**Whether it is Numpy or Torch, the array subscript starts from 0.**

- If you want to access a certain line, such as the first line, you can use [1, :].

- What does [1:3, 1:] mean?
It means, from the row it is to access the first and second row, from the column, it is to access after the first column.

- What about [::3, ::2] ?
It means accessing the data, one interval every 3 rows and every 2 columns.

- The shape of tensor([[[2,1,4,3],[1,2,3,4],[4,3,2,1]]]) is (1,3,4)

- x[-1] refers to the last row;
x[1:3] refers to the second row and the third row;
x[0:2, :]=12 means assigning the first row and the second row to 12.

**Broadcasting**
The shapes of two tensor are different, and they will be a broadcast.
- X.sum(axis=n): Add sum according to the direction of axis. In other words,remove the dimension value of the axis. 
For example, X.shape is (3,4,5), X.sum(axis=1).shape is (3,5).

- A.sum(axis=1,keepdims=True): Keepdims= true means that the value of axis could be retained.
For example, X.shape is (3,4,5), X.sum(axis=1,keepdims=True).shape is (3,1,5)


**Common coding operations**
```python
torch.arrange(12) #create a vector from 1 to 11
torch.zeros((2,3,4)) or torch.ones((2,3,4)) #create a tensor which shape is (2,3,4)
torch.zeros_like(Y) #create a zero tensor which shape is same to Y
tensor([[2,1,4,3,],[1,2,3,4],[4,3,2,1]]) #list of list


x.reshape(3,4) #'reshape(1,3,4)' is also allowed; It is continuous in the row.
torch.cat((x, y), dim=0) #like stacking it up by row

x.item #get the high-precision value of x
x.shape #the shape of x
x.numel() #the number of elemets
x.sum() #output is just a tensor
x.mean() #the average value of the whole x

x==y #tensor x and tensor y，there are as many return values as the elements.
id(x) #return the address of x
torch.exp(x) #do an exponential operation on x
float(x) and int(x) #forced type conversion

x.numpy() #from tensor to np.array
torch.tensor(x) #from np.array to tensor
```


### Data Pre-processing
- **Missing Data**
We usually have two methods, one is interpolation, the other is to delete incomplete data.
There is another method that we rarely use, we can regard NaN as a separate type.
```
inputs=inputs.fillna(inputs.mean())  #The simplest method is to fill nan with a mean
pd.get_dummies(inputs, dummy_na=true) #One hot encode. dummy_na refers to whether create a column of Nan. 
```
- **Difference between reshape and view**
reshape will not change the address.
For example, b=a.reshape(3,4), then we change the value of b, a will also be changed with b.
What's more, .clone() and .detach() have the similar characteristics.
```
B=A.clone() # B and A don't have the same address.
B=A.detach() # B and A have the same address.
```

- **Norm**
L2: torch.norm()
L1:
F-Norm:

- **Common coding operations**
```python
import os
os.makedirs(os.path.join(a,b,c),exit_ok=) #exit_ok means if the folder already exists, do nothing.
data_file=os.path.join("","",".csv") #os.path.join means stitching the path;
with open(data_file,"w") as f: #write=
	 f.write

import pandas as pd
data=pd.read_csv(data_file) #read the document of csv format

inputs, outputs=data.iloc[:,0:2],data.iloc[:,2] #iloc means index location

X.T #Transposition pf X

torch.mv(A, B) #matrix multiplies vector, (m,n)*(n,1)=(m,1)
torch.mm(A, B) #matrix multiplies matrix. (m,n)*(n,x)=(m,x)
```