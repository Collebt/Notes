## 求交集



输入两个列表，要求统计两个列表相同元素的数量。其中每个列表内的元素都是不重复的。最终性能提升了5000倍。

首先创建两个列表，并将元素的顺序打乱。



```python
from random import shuffle
arr1 = list(range(2000))
shuffle(arr1)
arr2 = list(range(1000, 3000))
shuffle(arr2)
```



将数组转为集合，求交集的长度。平均运行时间0.067毫秒

```python
def n_common_5(arr1, arr2):
    return len(set(arr1) & set(arr2))
%timeit n_common_5(arr1, arr2)
67.2 µs ± 755 ns per loop (mean ± std. dev. of 7 runs, 10000 loops each)

```

