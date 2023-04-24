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
- **Weight recession**
- **Regularization**
- **Dropout**
- **Change the labels**
