# 用表驱动代替switch

## lambda的作用

lambda作为一个表达式，定义了一个匿名函数，上例的代码x为入口参数，x+1为函数体，用函数来表示为

`lambda x:x+1(1)`

**用于代替switch**

```python

result = {
  'a': lambda x: x * 5,
  'b': lambda x: x+7,
  'c': lambda x: x-2
}

a = result['c'](6)
print(a)
```

建议少用，会导致易读性下降

# 表驱动用于遍历

**PCA中for x 表示遍历**

```python
dataset_len = {'train': 100, 'test': 30}
image_dataset = {
	x: GMDataset(
				sets=x,
				length=dataset_len[x],
				cls=cfg.TRAIN.CLASS if x == 'train' else None,
	for x in ('train', 'test')}#x={'train', 'test'}按顺序赋值
```

