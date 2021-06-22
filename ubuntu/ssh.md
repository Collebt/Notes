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

要达到的目的：
A机器ssh登录B机器无需输入密码；
加密方式选 rsa|dsa均可以，默认dsa



- 单向登陆的操作过程（能满足上边的目的）：

1、登录A机器
2、ssh-keygen -t [rsa|dsa]，将会生成密钥文件和私钥文件 id_rsa,id_rsa.pub或id_dsa,id_dsa.pub
3、将 .pub 文件复制到B机器的 .ssh 目录， 并 cat id_dsa.pub >> ~/.ssh/authorized_keys
4、大功告成，从A机器登录B机器的目标账户，不再需要密码了；（直接运行 **#ssh 192.168.20.60** ）

 

- 双向登陆的操作过程：

1、ssh-keygen做密码验证可以使在向对方机器上ssh ,scp不用使用密码.具体方法如下:
2、两个节点都执行操作：**#ssh-keygen -t rsa**
 然后全部回车,采用默认值.

3、这样生成了一对密钥，存放在用户目录的~/.ssh下。
**将公钥考到对方机器的用户目录下**，并将其复制到~/.ssh/authorized_keys中（操作命令：**#cat id_dsa.pub >> ~/.ssh/authorized_keys**）。