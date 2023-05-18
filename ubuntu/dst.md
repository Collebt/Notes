# dst server in Linux

更新饥荒服务器

```
sudo su
cd /home/steamcmd/
./steamcmd.sh
```



```
login anonymous
force_install_dir /home/steamcmd/dstserver (这里的/home/dstserver要改为你们自己的服务器路径)
app_update 343050 validate

```

重启服务器



```
cd /home/steamcmd/dstserver/bin
./master_start.sh
./cave_start.sh

```

