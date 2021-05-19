# pytorch的常用函数



## einsum

einsum可以用来计算矩阵的各种运算

### numpy 和 torch 的einsum比较

numpy的einsum速度要快很多，即使先将tensor转换成array进行einsum再转换回去，速度也很快。

速度比较：numpy快两个数量级( numpy-0.05 ;  torch-5.904)

在大张量的情况下更加明显，但有一个问题就是如果要经常用，不断切换格式也会很麻烦。



输入参数都是(equation, operands)

numpy的operands是变长参数列表

torch的operands是列表

### 注意事项expand

在输出的时候要注意不同的顺序可以使用广播简化后面的操作



### Reference

[Tim Rocktäschel]: https://rockt.github.io/2018/04/30/einsum

### 公式示例

转置$B_{ji}=A_{ij}$:`B = torch.einsum('ij->ji',A)`

sum: $b = \sum_i \sum JA_{ij}$:`b = torch.einsum('ij->',A)#标量不需要填下标`

sum colums: $b = \sum_j A_{ij}$:`b = torch.einsum('ij->j', A)`

sum rows: $b = \sum_i A_{ij}$: `b = torch.einsum('ij-i', A)`

矩阵-向量相乘: $c = ||Ab||_F^1 =\sum_k A_{ik} b_{k}$: `c = torch.einsum('ik,k->i ',[A,b])`

矩阵-矩阵相乘: $C = AB \to C_{ij} = \sum_k A_{ik} B_{kj}$: `c = torch.einsum('ik,k->i ',[A,b])`

点积：

- 向量点乘: $c = a_ib_i$: `c = torch.einsum('i,i->', [a,b])`
- 矩阵点乘: $C = A_{ij}B_{ij}$: `C = torch.einsum('ij,ij->ij', [A,B])`
- 向量外积: $C_{ij} = a_i b_j$: `C = torch.einsum('i,j->ij', [a, b])`



## tensor维度操作

### unsqueeze：用于广播前的准备

输入参数

`torch.unsqueeze(input, dim, out=None)`

常用操作：

`tensor.unsqueeze(dim)`

dim为插入维度的索引,对输入的索引维度增加维度1

```python
in = torch.ones(2,3,4,5) #in.shape=(2,3,4,5)
out1 = in.unsqueeze(1) #out1.shape = (2,1,3,4,5)
out2 = in.unsqueeze(-1)#在最后增加一个维度，out2.shape = (2,3,4,5,1)
```

 返回tensor共用原来的内存

### squeeze：用于降维

### 将输入变量中维度为1的维度去掉

`torch.squeeze(input,dim,out)`

输入的shape（A,1,B,C,1,D)

输出的shape（A,B,C,D)

 ```python
in = torch.ones(2,3,1,4,1,5) #in.shape=(2,3,1,4,1,5)
out1 = in.squeeze() #out1.shape = (2,3,4,5)
out2 = in.squeeze(1) #out2.shape = (2,3,4,1,5)
out3 = in.squeeze(2) #报错，in的第3维尺寸为4，不可删除
 ```



可以指定删除的维度，但该维度不为1时，不会删除维度。

 

目的：维度为1仅仅是扩充维度的作用，降维为了减少计算量



### 张量增加维度使用unsqueeze()

使用范围：在ndarray和tensor类型中可以使用，list无法使用（会报错）

>`[None, ...]` is **numpy notation** for `.unsqueeze(0)`. The two are equivalent. The version with advanced indexing might be a  bit slower because it has more checking to do to find out exactly what  you want to do. 

None和unsqueeze()是等价的，但由于unsqueeze()明确了插入的维度，因此速度更快，易读性更好

### None用于增加维度

加入None会在对应维度位置增加一维，但是由于没有显式标明增加的维度，导致可读性较差。

```python
a = np.ones([2,3,4])
b = a[None]#b.shape=(1,2,3,4)
c = a[:,None,:] #c.shape=(2,1,3,4)
#在这里不需要全部索引都输入，其实只用输入前面已经有的索引，后面的None就代表在前多少的位置插入一个维度,
d = a[:,None,None]#d.shape=(2,1,1,3,4)
```



### Tensor的维度顺序



N: batch

C: channel

H: height

W: width

 

Caffe 的Blob通道顺序是：NCHW;

Tensorflow的tensor通道顺序：默认是NHWC， 也支持NCHW，使用cuDNN会更快;

Pytorch中tensor的通道顺序：NCHW

TensorRT中的tensor 通道顺序： NCHW



但是在网路搭建中并不是固定的，视情况而改变。

比如在SuperGlue中，每一次输入的Tensor为一个图节点特征矩阵$F \in R^{n\times m}$，张量A=Tensor(b，m,n,1)，将其作为一维卷积模块`conv1d()`的输入，卷积的部分为m所在的向量。





------------------------------------------------

原文链接：https://blog.csdn.net/oLingFengYu/article/details/88033668



### 矩阵广播操作repeat

要注意在torch和numpy中的repeat扩展矩阵的参数是不相同的，最好固定一种使用方式。numpy中可以在ipad上的jupyter使用，

 

Torch.tensor: ` repeat(*sizes)->tensor`

 Numpy: `repeat(a,repeats,axis=None)`

输入参数：

`a: array_like input array      `

`repeats: the  number for broadcast num`

`axis: the  axis along with th repeat value ` 



## NN.Autograd

pytorch使用动态图，每一次计算都直接把计算图记录（通过`nn.autograd.functional`类函数保存和调出Tensor。



### Autograd.functional使用示例

```python
import torch
class MyReLU(torch.autograd.Function):
    """
    We can implement our own custom autograd Functions by subclassing
    torch.autograd.Function and implementing the forward and backward passes
    which operate on Tensors.
    """
@staticmethod
    def forward(ctx, input):
        """
        In the forward pass we receive a Tensor containing the input and return
        a Tensor containing the output. ctx is a context object that can be used
        to stash information for backward computation. You can cache arbitrary
        objects for use in the backward pass using the ctx.save_for_backward method.
        """
        ctx.save_for_backward(input)
        return input.clamp(min=0)
@staticmethod
    def backward(ctx, grad_output):
        """
        In the backward pass we receive a Tensor containing the gradient of the loss
        with respect to the output, and we need to compute the gradient of the loss
        with respect to the input.
        """
        input, = ctx.saved_tensors
        grad_input = grad_output.clone()
        grad_input[input < 0] = 0
        return grad_input
dtype = torch.float
device = torch.device("cpu")
# device = torch.device("cuda:0")  # Uncomment this to run on GPU
# torch.backends.cuda.matmul.allow_tf32 = False  # Uncomment this to run on GPU
# The above line disables TensorFloat32. This a feature that allows
# networks to run at a much faster speed while sacrificing precision.
# Although TensorFloat32 works well on most real models, for our toy model
# in this tutorial, the sacrificed precision causes convergence issue.
# For more information, see:
# https://pytorch.org/docs/stable/notes/cuda.html#tensorfloat-32-tf32-on-ampere-devices
# N is batch size; D_in is input dimension;
# H is hidden dimension; D_out is output dimension.
N, D_in, H, D_out = 64, 1000, 100, 10
# Create random Tensors to hold input and outputs.
x = torch.randn(N, D_in, device=device, dtype=dtype)
y = torch.randn(N, D_out, device=device, dtype=dtype)
# Create random Tensors for weights.
w1 = torch.randn(D_in, H, device=device, dtype=dtype, requires_grad=True)
w2 = torch.randn(H, D_out, device=device, dtype=dtype, requires_grad=True)
learning_rate = 1e-6
for t in range(500):
    # To apply our Function, we use Function.apply method. We alias this as 'relu'.
    relu = MyReLU.apply
# Forward pass: compute predicted y using operations; we compute
    # ReLU using our custom autograd operation.
    y_pred = relu(x.mm(w1)).mm(w2)
# Compute and print loss
    loss = (y_pred - y).pow(2).sum()
    if t % 100 == 99:
        print(t, loss.item())
# Use autograd to compute the backward pass.
    loss.backward()
# Update weights using gradient descent
    with torch.no_grad():
        w1 -= learning_rate * w1.grad
        w2 -= learning_rate * w2.grad
# Manually zero the gradients after updating weights
        w1.grad.zero_()
        w2.grad.zero_()

```





优点：它不管你进行了什么操作，只要涉及到（`required_grad=True`)的变量，就自动把计算图记录进去。

 

最后使用`Tensor.backward()`的时候，通过`nn.autograd.functional`的`backward()`函数反传计算梯度到每一个tensor中，把每个`required_grad=True`张量的梯度储存在该张量的grad中，并（默认）删除这次计算的计算图。

 **注意**：张量的grad不会自己删除，会一直叠加，需要用zero_grad()手动删除。



## NN.bmm

`torch.bmm(batch1, batch2, out=None)-> Tensor`

Perform a batch matrix-matrix product of matrices stored in `batch1` and `batch2`.

`batch1 `and `batch2` must be 3-D tensotr each containing the same number of matrices.

if `batch1` : $(b \times n \times m)$tensor， `batch2` :$(b \times n \times m)$tensor，`out` will be a $(b \times n \times p)$

​			$\text{out}_i = \text{batch1}_i @ \text{batch2}_i$

This function does not ==broadcast==. For broadcasting matrix products, see `torch.matmul()`

---

## nn.Linear 和 nn.Conv1d()的比较

`nn.Conv1d` with a kernel size of 1 and `nn.Linear` give exactly t**he same results**. The only differences are the  initialization procedure and how the operations are applied (which has  some effect on the speed). Note that using a linear layer should be  faster as it is implemented as a simple matrix multiplication (+ adding a broadcasted bias vector)

@RobinFrcd your answers are either different due to `MaxPool1d` or due to the different initialization procedure.

Here are a few experiments to prove my claims:

```python
def count_parameters(model):
    """Count the number of parameters in a model."""
    return sum([p.numel() for p in model.parameters()])

conv = torch.nn.Conv1d(8,32,1)
print(count_parameters(conv))
# 288

linear = torch.nn.Linear(8,32)
print(count_parameters(linear))
# 288

print(conv.weight.shape)
# torch.Size([32, 8, 1])
print(linear.weight.shape)
# torch.Size([32, 8])

# use same initialization
linear.weight = torch.nn.Parameter(conv.weight.squeeze(2))
linear.bias = torch.nn.Parameter(conv.bias)

tensor = torch.randn(128,256,8)
permuted_tensor = tensor.permute(0,2,1).clone().contiguous()

out_linear = linear(tensor)
print(out_linear.mean())
# tensor(0.0067, grad_fn=<MeanBackward0>)

out_conv = conv(permuted_tensor)
print(out_conv.mean())
# tensor(0.0067, grad_fn=<MeanBackward0>)
```

Speed test:

```python
%%timeit
_ = linear(tensor)
# 151 µs ± 297 ns per loop

%%timeit
_ = conv(permuted_tensor)
# 1.43 ms ± 6.33 µs per loop
```

结论: 使用linear速度更快





---

## 参数初始化

`nn.Parameter(Tensor) `

继承`torch.Tensor`, 用于设置可学习的参数，自动认为是可训练参数，加入到`parameter()`迭代器中



## Tensor.to()

`tensor.to(device) `将tensor的注册设备转换到指定的设备上

`tensor.to(dtype)`change the tensor's dtype(self.dtype) to dtype(optial) ,转换对应格式























 

