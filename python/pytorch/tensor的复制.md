# Tensor 的复制方法

## 复制形状 

- `y = trnsor.new_tensor(x)`
- `y = tensor.empty_like(x)`
- `y = x.clone().detach()`

```python
y = x.deepcopy()
```

## 复制数值

| # Operation             | New/Shared memory | Still in computation graph |
| ----------------------- | ----------------- | -------------------------- |
| tensor.clone()          | New               | Yes                        |
| tensor.detach()         | Shared            | No                         |
| tensor.clone().detach() | New               | No                         |

**使用clone():**
返回一个原张量的副本,同时不破换计算图,它能够维持反向传播计算梯度,
并且两个张量不共享内存.一个张量上值的改变不影响另一个张量.

- **但是梯度会流向原本的x,而不是clone_x.**

```python
x= torch.tensor([1., 2., 3.], requires_grad=True)
clone_x = x.clone()

f = torch.nn.Linear(3, 1)
y = f(clone_x)
y.backward()

print(x.grad)
print(clone_x.grad)
```

输出结果:

```python
tensor([-0.0043,  0.3097, -0.4752]) #原本的x的梯度
None #clone_x没有梯度
```





- **原始tensor设为==requires_grad=False==，clone()后的梯度设为.requires_grad_()，clone()后的tensor参与计算图的运算，则==梯度穿向clone()后的tensor==。**

```
x= torch.tensor([1., 2., 3.], requires_grad=False)
clone_x = x.clone().requires_grad_()

f = torch.nn.Linear(3, 1)
y = f(clone_x)
y.backward()

print(x.grad)
print(clone_x.grad)
```

输出结果:

```python
None #x取消记录梯度
tensor([-0.0043,  0.3097, -0.4752]) #梯度流向clone_x
```

原文链接：https://blog.csdn.net/winycg/article/details/100813519



**使用copy_():**
比如`x4.copy_(x2)`, 将x2的数据复制到x4,并且会
修改计算图,使得反向传播自动计算梯度时,计算出x4的梯度后
再继续前向计算x2的梯度. 注意,复制完成之后,两者的值的改变互不影响,
因为他们并不共享内存.



**使用detach():**
比如`x4 = x2.detach()`,返回一个和原张量x2共享内存的新张量x4,
两者的改动可以相互可见, 一个张量上的值的改动会影响到另一个张量.
返回的新张量和计算图相互独立,即新张量和计算图不再关联,
因此也无法进行反向传播计算梯度.即从计算图上把这个张量x2拆
卸detach下来,非常形象.



**使用detach\_():**
`detach()`的inplace版本,功能和detach()类似.
比如`x4 = x2.detach_()`,其实x2和x4是同一个对象,返回的是self,
x2和x4具有相同的id()值.


原文链接：https://blog.csdn.net/m0_46653437/article/details/112547756