# 关于Shell启动的设置

问题来源:

之前设置打字法的时候配置了shell的启动设置，但是后来安装不成功,就导致每一次打开shell都会出现以下的信息,让报错和强迫症都很难受。

在重新了解了shell的初始化原理之后，得到的解决方法如下：在以前配置了启动打字法的.profile文件中删除对应的启动命令。





每次启动一个新shell时，bash shell都会运行.bashrc文件。

随后依照下列顺序所找到的第一个文件会被运行。

```
$HOME/.bashrc 
$HOME/.bash_profile 
$HOME/.bash_login 
$HOME/.profile
```



bashrc中包含conda和cuda的初始化信息

而profile则包含打字法等初始化信息。