---
title: MLP
date: 2023-04-24 19:43:22
tags:
---

### Single Layer Perceptron
Input are x1,x2,...,xn, output is a single element.

SLP is **different** from **regression** in that regression's output is a real number, but SLP's output is a class.
SLP is **different** from **softmax** in that softmax's output is a probability.

SLP has a great **drawback**: It is unable to fix the XOR function.

### Multiple Layer Perceptron

**Why do we need a nonlinear activation function?**
If the activation function is linear function, such as f(x)=x.
h=w1x+b1
o=w2h+b2
Hence o=w2w1x+b
We can see that multiple FC layers linked together are still like a single FC layer.

**Activation Function**
- Sigmoid
- Tanh
- ReLU
ReLU is the most commonly used, because it is fast and easy to calculate and doesn't require exponential operation.

### Train,Test,Val
- Training dataset: training model parameters. **Training error**
- Validation dataset: the data can't be mixed with training data, select the hyperparameter.
- Testing dataset: A new dataset that is only used once. **Generalization error**

### Gradient Descent
- SGD
- Adam: insensitive to learning rate.
**If the error in training cannot be measured by the difference between the real value and the predicted value, we should pay attention to the relative error.**
Use the real value divided by the predicted value and take a log then use the loss function. If the prediction is the same as the real value, it is ln1 and the loss is 0.

### K-Flod cross validation
This is a method used to adjust hyperparameters. K is usually seted to 5 or 10.
**step1** define the k value, such as 5.
**step2** split the dataset into 5 parts. 4 parts of them are viewed as training data, 1 part of them is viewed as validation data.
**step3** use the data train the model. We will get 5 trained models finally.
**step4** average its score on the validation dataset respectively. Record the score and the value of hyperparameters.
**step5** change the hyperparameters and **repeat step1-step4**.
**step6** select the highest score and fix its hyperparameters.
**step7** use all dataset to train the model with fixed hyperparameters again

### Overfitting and Underfitting
Underfitting shows that the capacity of model is relatively large. Thus, overfitting is not absolutely a bad thing.

It is **impossible** to compare model capacity between different types of algorithms, such as trees and neural networks. If they are the same type, the following factors can be compared: 1. the number of parameters 2. the range of parameter values. 

**VC dimension**: The size of a largest dataset that the model can record. For example, the VC dim of single layer perceptron is 3.(XOR function has 4 points)

**Evaluation criteria for data complexity**
- number of samples
- elemental structure of samples
- time and space structure
- diversity of samples

### The Methods of Avoiding Overfitting
**Regularization**
The purpose of regularization is to reduce generalization errors. This is a way to reduce overfitting.

- **Weight recession**
Set a hyperparameter to constrain the range of model parameters through the L2 Regularization. The value of hyperparameters is usually set to 0.001. 
**Concise Usage** use the parameter named "weight_dacay" in the "optim" 

- **Dropout**
This way may slow down the convergence. The value is usually set to 0.1, 0.5 or 0.9. It's like adding noise between layers. When coding, we can turn off dropout layer by "is_training=0".
**Dropout layer is designed for FC layer, and BN is for the convolutional layer.**
Dropout layer has P chance of putting the parameters at 0 and has (1-p) chance of dividing the parameters by (1-p).
Dropout only takes effect in training. When infering, the output is just the input.

- **Change the labels**
Randomly modify the label to add noice to the model training.

### Numerical stability
- Gradient explosion
1. The value exceeds the range.(Nvidia adopts 16-bit floating-point numbers)
2. **Too sensitive to learning rate.** If learning rate is too big, the large parameter will lead to a larger gradient and the gradient will exceeds the range easily. If learing rate is too small, the training will make no progress.

- Gradient disappears
The gradient value becomes 0.

**Ways to solve the problems above**
1. change the multiplication to the addition. Such as ResNet and LSTM.

2. **Normalize the gradient** Gradient cutting.

3. **Reasonable weight initialization and activation function**
The output and gradient of each layer can be regarded as ramdom variables. We should keep their mean and variance consistent.

**Xavier initial**
Let the input and output obey the same distribution as much as possible.
```python
torch.nn.init.xavier_uniform_(tensor: Tensor, gain: float = 1.)
torch.nn.init.xavier_normal_(tensor: Tensor, gain: float = 1.)
```

After derivation, we can kown that **when the activation function is equivalent to f(x)=x, it works best.**
According to the Talor expansion, **Tanh** and **ReLU** meet the requirement near 0. We can also improve the **Sigmoid**, as **4*sigmoid(x)-2**.

