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
**Missing Data**
We usually have two methods, one is interpolation, the other is to delete incomplete data.
There is another method that we rarely use, we can regard NaN as a separate type.
```
inputs=inputs.fillna(inputs.mean())  #The simplest method is to fill nan with a mean
pd.get_dummies(inputs, dummy_na=true) #One hot encode. dummy_na refers to whether create a column of Nan. 
```
**Difference between reshape and view**
reshape will not change the address.
For example, b=a.reshape(3,4), then we change the value of b, a will also be changed with b.
What's more, .clone() and .detach() have the similar characteristics.
```
B=A.clone() # B and A don't have the same address.
B=A.detach() # B and A have the same address.
```

**Norm**
L2: torch.norm() points to the sum of the squares of each element and then find the square root.
L1: The sum of absolute values.
F-Norm: The root value of the sum of the squares of each item in the matrix.

**Constructor**
- construct ordinary functions:
from mxnet import sym
a= sym.var()
This is an explicit structure: Write down the formula first, and then give the value.

- Implicit construction
from mxnet import autogrid, nd
With autogrid.record():
	a=nd.ones((2,1))
	b=nd.ones((2,1))

- Chain rule
Positive accumulation: Memory complexity O(1); Computational complexity O(n).
Reverse transfer: Need to save all forward values. Memory complexity O(n).

We can use the code: x.requires_grad(True) to save the grad of x, and use the code: x.grad to view x's grad.Then we can use the code: x.backward() to complete the derivation.
If we don't need the gradient, we can use the code:detach to delete the gradient.

Generally speaking, pytorch will accumulate the gridients. This has both advantages and disadvantages.
Adavantage: if we don't have enough memory for caculating a batch, we can break the batch down into many small parts.
Disadvante: we need use the code: x.grad.zero_() to empty the gradient.

**Loss Function**
L1 Loss: Absolute value loss. Whatever the gap, the update speed is stable.
L2 Loss: Average square loss. The gap is larger, the update speed is faster.
Huber's robust loss: combine the two loss function above.

Softmax+Cross Entropy: loss=-log(y_prediction); Cross Entropy only pays attention to the value of the element corresponding to the real value.

**Optimization Method**
Small batch random gradient descent: Randomly sample n samples to approximate the loss.
Theoretically speaking, because of the noise, the smaller the batch-size is, the effect is better.

We should make sure that the data reading speed is faster than the training speed before training. The code listed below could be used:
	time=d2l.Timer()
	For x,y in train_iter:
	Continue
	F’{timer.stop():.2f} sec’
	
**Common coding operations**
```python
import os
os.makedirs(os.path.join(a,b,c),exit_ok=) #exit_ok means if the folder already exists, do nothing.
data_file=os.path.join("","",".csv") #os.path.join means stitching the path;
with open(data_file,"w") as f: #write=
	 f.write

import pandas as pd
data=pd.read_csv(data_file) #read the document of csv format

inputs, outputs=data.iloc[:,0:2],data.iloc[:,2] #iloc means index location

y=torch.tensor([0,2])
y_hat[[0,1],y] #take out the element of subscript 0 of sample 0 and the element of subscript 2 of sample 1.

X.T #Transposition pf X

torch.mv(A, B) #matrix multiplies vector, (m,n)*(n,1)=(m,1)
torch.mm(A, B) #matrix multiplies matrix. (m,n)*(n,x)=(m,x)
torch.dot(,) #Internal product x1y1+x2y2+x3y3

torch.normal(mean,std,size) #std means standard deviation

data.tensordataset
data.dataloader
nn.sequential()
```