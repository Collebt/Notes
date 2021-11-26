# 坚果云+Zotero同步+papership

用于同步论文管理



<img src="image-20210414145118464.png" alt="image-20210414145118464" style="zoom: 80%;" />

账户：collebt

密码：whu****

选择 WebDAV

- 打开坚果云网页->右上角账号信息->安全选项

![image-20210414144946841](image-20210414144946841.png)

往zotero中填写服务器地址，账号，密码即可。



## Papership 是ipad端的论文管理器

有时候会出现无法验证服务器的情况，如论文上传失败或者验证服务器失败。

解决方法：

​	打开坚果云官网，登录坚果云账号，在`zotero`文件夹新建空白的`lastsync.txt`文件，务必注意的是，必须使用坚果云**自带的新建文件工具**来新建`lastsync.txt`文件。`	重新在`Zotero`客户端或者`Papership`验证服务器即可

## 注意事项

在使用ubuntu版本时，如果开启了VPN的代理，会导致zotero无法同步，需要手动关闭vp才能同步。

或者设置VPN规则，将zotero的联网设为直连模式。

