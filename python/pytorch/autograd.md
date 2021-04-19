## 对于反传方程中的next_functions的理解

Regarding your question, the next_functions will allow you to traverse the recorded calculation graph (“backward graph”).
**The backward graph will end in AccumulateGrad nodes for the leaves (they have a `.variable` attribute pointing to the leaf tensor)** - and yours does pretty quickly as you only have one operation. Let’s have a slightly more elaborate one:

```python
a = torch.randn(1, requires_grad=True)
b = a*(a+2)
print (b.grad_fn.next_functions)
print (b.grad_fn.next_functions[1][0].next_functions)
print (b.grad_fn.next_functions[0][0].variable is a)
```

gives

```
((<AccumulateGrad object at 0x7fbe7aa96780>, 0), (<AddBackward0 object at 0x7fbe7aa96748>, 0))
((<AccumulateGrad object at 0x7fbe7aa96780>, 0), (None, 0))
True
```

So in `x*(x+2)` you have one branch for `x` and one for `x+2` and the latter has a `x` branch and an uninteresting `2` branch.
Except at the leaves, you cannot, in general access the variables of the calculation from the graph.