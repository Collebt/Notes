# TensorboardX

- add_graph
    [example](https://github.com/lanpa/tensorboardX/blob/master/examples/demo_graph.py)

- tourtial
    [get start](https://www.tensorflow.org/tensorboard/get_started)



**绘制网络节点图**

```python
fromTensorboardX import SummaryWriter

with SummaryWriter(comment='LinearInLinear') as w:
  w.add_graph(LinearInLinear(), dummy_input, True)

 
```

 

**绘制同一行的图像**

```python
#使用统一个文件夹目录"train"
tfboard_writer.add_scalars(
    'train/loss', loss_dict, epoch * cfg.TRAIN.EPOCH_ITERS + iter_num)
tfboard_writer.add_scalars(
    'train/training accuracy', accdict, epoch * cfg.TRAIN.EPOCH_ITERS + iter_num )
```

得到目录后 

进入runs目录， 输入

```bash
tensorboard --logdir mylogdir
```

- 指定端口和文件夹

```
tensorboard --logdir=/tmp  --port=8008
```



## add_scalar

用于记录loss和画曲线图，主要函数



 ## add_graph

- 可视化神经网络的变量

- 运行图

感觉这个作用其实并不大,操作节点(opNode)大部分为数字编号，难以分辨具体的操作

 

用于查看网络变量流程图



对于不同的操作/网络结构设计，在graph上是不一样的，这个后面做训练去熟悉一些简单的可视化，如多输入多输出，多层，迭代，Siames等。

[网络教程]https://github.com/lanpa/tensorboardX/blob/master/examples/demo_graph.py



## 出现问题和解决方法

**问题**：网络的图像没有办法输出，跑完之后没有报错，但是就是没有具体的图像，文件大小2.8kb

 

**原因和解决方法**: tensorboardX版本问题，重新卸载后安装就可以了