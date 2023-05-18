## 开放http端口

在实验室方便使用overleaf，需要开放实验室服务器的端口到内网。

里面的1883就是要开放的端口号

```
#安装iptables
apt-get install iptables

#开放端口
sudo iptables -I INPUT -p tcp --dport 1883 -j ACCEPT

#保存
sudo iptables-save
```

