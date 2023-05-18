## .多个 cuda 版本之间进行切换

将~/.bashrc 或　~/.zshrc 下与cuda相关的路径都改为　/usr/local/cuda/　而不使用　/usr/local/cuda-8.0/ 或/usr/local/cuda-9.0/。

- 方法一：更改用户自己的cuda路径。`gedit ~/.bashrc`打开.bashrc
- 注意要加双引号

```
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda-11.1/lib64"
export PATH="$PATH:/usr/local/cuda-11.1/bin"
export CUDA_HOME="$CUDA_HOME:/usr/local/cuda-11.1"
```

`sh .bashrc` 更新配置文件，并重启窗口。

- 方法二：改变全局的默认cuda路径（不推荐，会影响到其他的用户）

```
#在切换cuda版本时
sudo rm -rf /usr/local/cuda#删除之前创建的软链接
sudo ln -s /usr/local/cuda-8.0/ /usr/local/cuda

nvcc -V #查看当前 cuda 版本
```


原文链接：https://blog.csdn.net/Maple2014/article/details/78574275



## 在bin上装过cuda的情况

我自己因为在`/usr/lib/nvidia-cuda-toolkit`中安装了10.1版本的cuda，因此在matlab的gpu coder中会因为版本过低而报错，因此需要更换版本。在usr/local/中安装了11.4和11.6版本的cuda，但是使用上面的方并不能更换版本。（nvcc -V一直显示10.1版本）



并且在local中也找不到10.1版本的cuda，最后进行find搜索nvcc发现了在lib中的cuda，并且启动方式在`/usr/bin/nvcc`中。



我用了一种呢很简单粗暴的方法，就是将bin中的nvcc屏蔽掉。

```
sudo mv nvcc nvcc.bak
```

之后再输入`nvcc -V`就可以显示出11.6版本了。







## 更换cuda环境



cuda 11.1

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.1/lib64
export PATH=$PATH:/usr/local/cuda-11.1/bin
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-11.1
```



cuda10.0



```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.0/lib64
export PATH=$PATH:/usr/local/cuda-10.0/bin
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-10.0
```





## CUDA download

直接在官网下载runfile最方便.

以下为安装cuda11.8：

```
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
sudo sh cuda_11.8.0_520.61.05_linux.run
```

