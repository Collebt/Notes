服务器需要安装**ssh-server**才能登录

 

```bash
apt-get install openssh-server #安装ssh服务器

sudo ufw status%保证防火墙关闭
```

 

免密登陆

```bash
ssh-keygen #生成密钥
# 密钥初始目录 /home/username/.ssh
```

分发公钥id_ras.pub



- 密钥管理

--- .ssh

​	--- id_rsa #本机生成的私钥

​	--- id_rsa.pub #本机生成的公钥

​	--- server1name/ #用于存放服务器server1的公钥

​		---  id_rsa.pub #server1的公钥

​	--- server2name/ #用于存放服务器server1的公钥

​		---  id_rsa.pub #server2的公钥	

