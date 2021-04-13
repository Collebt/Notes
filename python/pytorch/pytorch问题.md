# 报错问题和解决方案



### Thread:ValueError: singal number 32 out of range

dataiter = iter(trainloader)

解决方法： 设置num_worker=0， 但是该方法治标不治本，会导致训练速度下降。

是python版本的问题， 可以重装python，这里凸显了安装环境的重要性。



### RuntimeError: expected scalar type Double but found Float

**原因**：tensor的数据类型不正确

**解决方法**： 将数据类型转为float32, 不要直接转换成double。



### Input type(torch.cuda.floatTensor) and weight type (torch.FloatTensor) should be then same

**原因**：输入数据放在gpu上，但是模型参数是在cpu上，导致类型不一致

**解决方法**：Model.to('cude') 有效。Model.cuda() 使用后好像还是报错



### 测试模型时出现error:incalid device id

台式主机只有一个gpu，所以设置的ngpu不能大于1。

服务器有多个gpu，可以设置大于1的



### Error:cant't convert cuda:0 device type tensor to numpy. Use Tensor.cpu() to copy tensor to host memory first.

输出数据无法画图，报错error:cant't convert cuda:0 device type tensor to numpy. Use Tensor.cpu() to copy tensor to host memory first.



**原因**：数据在gpu的内存上，需要使用data.cpu()转移回cpu内存上，在转化成numpy格式

numpy不能读取cuda tensor，需要转变成cpu tensor

**解决方法**：输入data.cpu().detach().numpy()



### ValueError: Expected more than 1 value per channel; when training, got input size[1, 32, 1]

32是中间隐藏层的大小，dim=2的1就是batch的channel数，channel数量太少（只有1个）导致无法进行batchNorm。

是输入样本大小波动产生的问题，如果设计网络的时候有些样本没有出现这种错误，那要往前去查找导致生成的channel只有1的情况。