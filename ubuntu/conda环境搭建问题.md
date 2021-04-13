报错conda commend not found

原因是因为~/.bashrc文件没有配置好

 

vim ~/.bashrc

添加

```
export PATH=$PATH:/home/wh/anaconda3/bin
```

(a 为insert模式，ctrl+C进入编辑画面， ":wq"保存退出

`sudo source ~/.bashrc`

再运行`conda info --envs`，出现提示即为成功

