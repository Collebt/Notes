# 局域网overleaf配置

最近想用latex做多人周报，考虑到以后写论文都要用latex，而且周报和所以想统一



[部署私有在线Latex编辑器:Overleaf/sharelatex](https://www.bilibili.com/read/cv6547551)

- 通过安装sharelatex使本地服务器使用overleaf成为可能
- latex多人编辑方便团队合作
- latex的函数功能可以动态调用子文件



想要实现的功能：

1. 最重要的是脱离平台的在线编辑功能，任何联网的机器都能够进行latex编辑和浏览。(v)
2. 分级操作权限和私人编辑区域，每个人只能够编辑自己的部分，可以浏览但不会修改他人的文件。(v)
3. 历史数据库，每一次的周报都有对应的版本记录。
4. 交互讨论，交互引用，可以浏览他人的文件并进行引用。







## 本地在线安装overleaf

1. 安装Docker

   ```bash
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   pip install docker-compose
   ```

   查看版本，检查是否安装成功 

   ```
   docker --version
   docker-compose --version
   ```

   

2. 安装overleaf

   ```
   sudo docker pull sharelatex/sharelatex
   ```

3. 获取配置

   ```bash
   wget https://raw.githubusercontent.com/sharelatex/sharelatex/master/docker-compose.yml
   ```

4. 在yaml文件目录下创建container

   ```
   sudo docker-compose up -d #只运行一次，否则可能会覆盖原本的container
   ```
   
   或者可以直接用指令创建容器

   ```
   docker run -d --name shareredis redis:latest
   docker run -d --name sharemongo mongo:latest
   docker run -d \
    -v ~/sharelatex_data:/var/lib/sharelatex \
    -p 5000:80 \
    --env SHARELATEX_MONGO_URL=mongodb://mongo/sharelatex --env SHARELATEX_REDIS_HOST=redis \
    --link sharemongo:mongo --link shareredis:redis \
    --name=sharelatex \
    sharelatex/sharelatex
   ```



5. 进入容器并安装完整texlive

   ```
   docker exec -it sharelatex bash #进入container
   tlmgr update --self --all
   tlmgr install scheme-full & 
   ```

   如果过慢可以尝试换源 

   ```
   tlmgr option repository https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/ 
   tlmgr update --self --all
   tlmgr install scheme-full & 
   ```



6. 修改服务器输出端口（在已经启动的情况下）

   1. 退出容器 `root@ed09e4490c57:/# exit`
   1. Stop the container (`docker stop <container_name>`).
   2. Change the file `config.v2.json` and `hostconfig.json`.
   3. Restart your docker engine (`service docker restart`).
   4. Restart the container (`docker restart <container_name>`).

   ```json
   vim /var/lib/docker/containers/ID/config.v2.json #docker
   vim /var/snap/docker/common/var-lib-docker/containers/ID/config.v2.json #docker #docker.socket
   
   "Config": {
       ....
       "ExposedPorts": {
           "80/tcp": {},
           "8888/tcp": {}
       },
       ....
   },
   "NetworkSettings": {
   ....
   "Ports": {
        "80/tcp": [
            {
                "HostIp": "",
                "HostPort": "80"
            }
        ],
   ```

   ```
   vim hostconfig.json
   
   "PortBindings": {
        "80/tcp": [
            {
                "HostIp": "",
                "HostPort": "80"
            }
        ],
        "8888/tcp": [
            {
                "HostIp": "",
                "HostPort": "8888"
            } 
        ]
    }
   ```

   

打开浏览器访问http://hostname:5000/launchpad，创建Admin账户 



进入容器方法

   ```
docker exec -it <容器 ID> /bin/bash 
   ```

## 简单配置中文环境

https://yxnchen.github.io/technique/Docker%E9%83%A8%E7%BD%B2ShareLaTeX%E5%B9%B6%E7%AE%80%E5%8D%95%E9%85%8D%E7%BD%AE%E4%B8%AD%E6%96%87%E7%8E%AF%E5%A2%83/#%E9%85%8D%E7%BD%AE%E4%B8%AD%E6%96%87%E5%86%99%E4%BD%9C%E7%8E%AF%E5%A2%83

## latex 管理员创建用户

管理员创建

```
# Overleaf Toolkit users:
$ bin/docker-compose exec sharelatex /bin/bash -c "cd /var/www/sharelatex; grunt user:create-admin --email=joe@example.com"

# legacy docker-compose.yml users:
$ docker exec sharelatex   -c "cd /var/www/sharelatex; grunt user:create-admin --email=joe@example.com"

```



普通用户创建

```
# Overleaf Toolkit users:
$ bin/docker-compose exec sharelatex /bin/bash -c "cd /var/www/sharelatex; grunt user:delete --email=joe@example.com"

# legacy docker-compose.yml users:
$ docker exec sharelatex /bin/bash -c "cd /var/www/sharelatex; grunt user:delete --email=joe@example.com"
```



在admin的管理用户界面中可以直接创建用户







## 用frp跳转到公网

**实现将实验室的latex公布到公网**

- 下载frp

- 修改映射服务器地址

vim **frpc**.ini

```ini
server_addr = 139.224.114.64
server_port = 7000
token = 861024


[overleaf]
type = tcp
local_ip = 127.0.0.1  sdkkjs
local_port = 8888 #这里初始是80端口
remote_port = 8888
```



- 后台运行启动frp

```
./frpc -c frpc.ini
```
- 关闭进程

```
ps -aux|grep frp |grep -v grep
kill -9 [对应port]
```



## 数据备份

首先找到配置路径中的sharelatex-data, mongo_data, redis_data 保存，然后在新服务器的对应位置重新覆盖原文档。



配置路径参数在 /var/lib/docker/containers/ID/ hostconfig.yaml （对应容器的启动参数）里面。ID是对应容器的ID号

但是在移动过后，可能会出现无法编译的情况。

#用回原本docker.socket里面的sharerelatex，就可以用了



## 在线latex的优势

优势：速度更快，网络更加稳定。档案维护方便

不足（这个通过frp解决了）：实验室有时候局域网不够稳定，没有专人维护，备份麻烦。在校外需要easyconnect

[Creating and managing users · overleaf/overleaf Wiki (github.com)](https://github.com/overleaf/overleaf/wiki/Creating-and-managing-users)

## 目前的问题&解决方案

1. github的同步还没有办法实现
2. texlive版本的控制没有实现





# 服务器Docker信息(1.0.0)





## 网络连接

实验室内网： 90.0.0.21:8888

校园网：202.114.107.125:9988

公网：139.224.114.64:8888



## 容器信息

容器位置：/var/snap/docker/common/var-lib-docker/container

容器开机自启动

容器信息：

```bash
wh@wh-ubuntu:~$ docker ps -a
CONTAINER ID   IMAGE                   COMMAND                  CREATED        STATUS         PORTS                                   NAMES
f44a2f458699   sharelatex/sharelatex   "/sbin/my_init"          44 hours ago   Up 4 minutes   0.0.0.0:8888->80/tcp, :::8888->80/tcp   sharelatex
bd58670906ec   mongo:latest            "docker-entrypoint.s…"   44 hours ago   Up 4 minutes   27017/tcp                               sharemongo
83814a2f5fd6   redis:latest            "docker-entrypoint.s…"   44 hours ago   Up 4 minutes   6379/tcp                                shareredis
```





## 修改容器启动参数

sharelatex  需要重启机器才能修改参数（以后看看有没有方法可以关闭socket并开启的）

```
vim /var/snap/docker/common/var-lib-docker/containers/ID/config.v2.json
# 修改对应参数
#sudo reboot
```



## 数据位置

sharelatex：

```
/home/wh/sharelatex_data
```

mongo:

```
/home/wh/mongo_data
```







http://90.0.0.21:8888/7363986933ytypkqkgvzdg
