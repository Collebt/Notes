# 使用eval实现灵活定义类

## eval()操作

`eval(expression[, globals[, locals]])`用于将字符串

eval() 函数用来执行一个字符串表达式，并返回表达式的值。

- expression -- 表达式。
- globals -- 变量作用域，全局命名空间，如果被提供，则必须是一个字典对象。
- locals -- 变量作用域，局部命名空间，如果被提供，可以是任何映射对象。



## 使用eval灵活定义类

在使用不同数据集时,通常对对应的数据集构建一个类.

比如对于pascal_voc构建一个Pascal的类,对willow构建一个Willow类



如果有很多个类,如何将类定义到变量中.

- 普通的方式是做if判断:

```

name = 'pascal'
if name == 'pascal':
	dataset = Pascal()
elif name == 'willow':
	dataset = Willow()
	
```

但是这样会让代码变得冗余复杂,当数据集增多时,需要修改上面的代码,明显增加工作量.



- 使用eval()生成类

```
name = 'Pascal' # or name = 'Willow'
dataset = eval(name)() #等价于dataset = Pascal() 或 dataset = Willow()
```



- 当需要输入参数时

```
name = 'Pascal' # or name = 'Willow'
dataset = eval(name)(**args) #等价于dataset = Pascal() 或 dataset = Willow()
```

