---
title: Deeplearning-Operation
date: 2023-04-24 14:30:40
tags:
---
### super().__init__()
This content comes from: https://www.codingem.com/super-in-python/

We can use super() to access the elements of a parent class. For example,
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def introduce(self):
        print(f"Hello, my name is {self.name}. I am {self.age} years old.")
# Subclass 1.
class Student(Person):
    def __init__(self, name, age, graduation_year):
        super().__init__(name, age)
        self.graduation_year = graduation_year
    
    def info(self):
        # Call the Person classes introduce() method to introduce this Student.
        super().introduce()
        print(f"{self.name} will graduate in {self.graduation_year}")
        
alice = Student("Alice", 30, 2023)
alice.info()
```
The output is:
```
Hello, my name is Alice. I am 30 years old.
Alice will graduate in 2023
```
We can access all the propertires in the parent class via the super() method.

### nn.Sequential
nn.Sequential defines a special kind of module.
nn.Sequential can be created by ourselves, the code is listed below.
```python
class MySequential(nn.Module):
    def __init__(self, *args):
        super().__init__()
        for block in args:
            self._modules[block]=block

    def forward(self, X):
        for block in self._modules.values():
            X=block(X)
        return X
```

We can use nn.Sequential directly:
```python
net = nn.Sequential(nn.Linear(20,256),nn.ReLU(),nn.Linear(256,10))
```

What's more, nn.Sequential can be nested used. We can define a class first, which includs nn.Sequential. Then, we define a new nn.Sequential which includes the nn.Sequential created above.
```python
class NestMLP(nn.Module):
    def __init__(self):
        super().__init__()
        self.net = nn.Sequential(nn.Linear(20, 64), 
                                 nn.ReLU(),
                                 nn.Linear(64, 32), nn.ReLU())
        self.linear = nn.Linear(32, 16)

    def forward(self, X):
        return self.linear(self.net(X))

chimera = nn.Sequential(NestMLP(), nn.Linear(16, 20), FixedHiddenMLP())
chimera(X)
```

If we used nn.Sequential to create the net, the name is default, such as the code above. The Linear is 0, the Relu is 1 and so on.
If we need to name the block, we can use the code listed below.
```python
def block1():
    return nn.Sequential(nn.Linear(4, 8),
                         nn.ReLU(), 
                         nn.Linear(8, 4),
                         nn.ReLU())

def block2():
    net = nn.Sequential()
    for i in range(4):
        net.add_module(f'block {i}', block1())
    return net

rgnet = nn.Sequential(block2(), nn.Linear(4, 1))
rgnet(X)
```
.add_module function can help us do the block naming.

### Custom layer
We can define the layer whatever we want, such as the layer of none parameters or the layer of paramerters. We could combine the layers we created as components to build more complex models.
```python
class CenteredLayer(nn.Module):
    def __init__(self):
        super().__init__()

    def forward(self, X):
        return X - X.mean()

layer = CenteredLayer()

class MyLinear(nn.Module):
    def __init__(self, in_units, units):
        super().__init__()
        self.weight = nn.Parameter(torch.randn(in_units, units))
        self.bias = nn.Parameter(torch.randn(units,))

    def forward(self, X):
        linear = torch.matmul(X, self.weight.data) + self.bias.data
        return F.relu(linear)

linear = MyLinear(5, 3)

net = nn.Sequential(nn.Linear(8, 128), CenteredLayer())
```

### forward function
We can define anything in the part of forward.
For example,
```python
class FixedHiddenMLP(nn.Module):
    def __init__(self):
        super().__init__()
        self.rand_weight = torch.rand((20, 20), requires_grad=False)
        self.linear = nn.Linear(20, 20)

    def forward(self, X):
        X = self.linear(X)
        X = F.relu(torch.mm(X, self.rand_weight) + 1)
        X = self.linear(X)
        while X.abs().sum() > 1:
            X /= 2
        return X.sum()

net = FixedHiddenMLP()
net(X)
```

### Parameter Accessing
- print(net(X))
print the output of net, when the input is X.
I don't think it is useful.

- print(net)
print the structure of the net.

- print(net[2].state_dict())
view all parameters in the third part of the net.

- print(net[2].bias.data)
view the parameter of the net.

- print(*[(name, param.shape) for name, param in net.named_parameters()])
view the name and shape of all the parameters in the net

### Initialization
If the layer is Linear layer, we can use this to initialize the weight and bias.
```python
def init_normal(m):
    if type(m) == nn.Linear:
        nn.init.normal_(m.weight, mean=0, std=0.01)
        nn.init.zeros_(m.bias)

net.apply(init_normal)
net[0].weight.data[0], net[0].bias.data[0]
```

We can also use constants to initialize weights and bias. This is useless though, just an example.
```python
def init_constant(m):
    if type(m) == nn.Linear:
        nn.init.constant_(m.weight, 1)
        nn.init.zeros_(m.bias)

net.apply(init_constant)
net[0].weight.data[0], net[0].bias.data[0]
```

Xavier is a common method to initialize the weight. First, we need to define the function to judge whether it is a Linear layer or not. Then we can use .apply to deal with all the weight in the Linear layer. For more details about xavier, please see the next chapter.
```python
def xavier(m):
    if type(m) == nn.Linear:
        nn.init.xavier_uniform_(m.weight)

net[0].apply(xavier)
```

On top of the default initialization method, we can definitely define the method of our own.
```python
def my_init(m):
    if type(m) == nn.Linear:
        print(
            "Init",
            *[(name, param.shape) for name, param in m.named_parameters()][0])
        nn.init.uniform_(m.weight, -10, 10)
        m.weight.data *= m.weight.data.abs() >= 5
net.apply(my_init)
net[0].weight[:2]
```
nn.init.uniform_(tensor, a, b):Fills the input Tensor with values drawn from the uniform distribution U(a,b).
The uniform distribution in the explanation means '均匀分布'.

We can also just add or subtract the weights.
```python
net[0].weight.data[:] += 1
net[0].weight.data[0, 0] = 42
net[0].weight.data[0]
```

If we hope two blocks in the module have the same parameters, we can deine the block first and call the block in the nn.Sequential then.
```python
shared = nn.Linear(8, 8)
net = nn.Sequential(nn.Linear(4, 8),nn.ReLU(),
                    shared,
                    nn.ReLU(),
                    shared,
                    nn.ReLU(),nn.Linear(8, 1))
```

### read & write
- tensor
torch.save(x, 'x-file')
x2 = torch.load('x-file')

- list of tensor
torch.save([x, y], 'x-files')
x2, y2 = torch.load('x-files')

- dictionary
torch.save(mydict, 'mydict')
mydict2 = torch.load('mydict')

- model parameters
torch.save(net.state_dict(), 'mlp.params')
clone.load_state_dict(torch.load('mlp.params'))