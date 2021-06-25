



 [Error: No such file (sftp liximomo extension)s](https://stackoverflow.com/questions/67506693/error-no-such-file-sftp-liximomo-extension)

打开 ~/.vscode/extensions/liximomo.sftp-1.12.9/node_modu

les/ssh2-streams/lib/sftp.js

在每一个`optionsza = false;`下面增加:

```
options.autoDestroy = false;
```



# vscode 端口转发

有时候在使用远程服务器进行开发的时候,需要使用端口进行某些操作:比如看tensorboard的loss图,如果在本地的电脑是直接打开localhost:6600就可以打开网页. 但是在远程的服务器就不能这样,所以需要将服务器的端口转发到本地的端口.



端口转发分为两种: 暂时性的和长久配置

暂时的端口转发用于临时占用某个端口,用完就销毁.

在Forwarding Ports 中



通常使用长期的配置:

在.ssh/.config中进行配置

```
Host microsoft_in
    HostName 90.0.0.245
    User lihaoyuan
    IdentityFile "/home/wh/.ssh/microsoft/id_rsa.pub"
    LocalForward 127.0.0.1:3000 127.0.0.1:3000 #将远程的3000端口转发到本地的3000端口
    
```

