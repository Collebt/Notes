遍历输出list或者tensor的元素：

使用join

```
print(' '.join(['head'] + [f'{acc:2.f}.ljust(5) for acc in acc_list]'))
```

