# 接口API

### 用户登录

#### 请求内容

请求消息

```
POST
/api/mgr/customers
```

请求参数

```
{
	"action":"login",
    "data":{
        "username":"用户唯一的名称",
        "password":"密码"
    }
}
```

#### 响应内容

http 响应消息 body 中， 数据以json格式存储，

如果添加成功，返回如下

```json
{
    "status": 0,
    "userdata":{
        "id" : 用户id(int),
        "username":"用户名称",
        "usertype": '1' '100' '2000' '3000' "用户状态（是否会"
    }
}
```

ret 为 0 表示成功。

id 为 添加客户的id号。

如果添加失败，返回失败的原因，示例如下

```json
{
    "status": 1,    
    "msg": "客户名已经存在"
}
```

ret 不为 0 表示失败， msg字段描述添加失败的原因



### 展示用户

请求消息

```
GET
/api/mgr/customers

```

请求参数

```
action = list_customer
```



### 注册用户

请求消息

```
POST
/api/mgr/customers
```

请求参数

```json
{
	"action":"add_customer",
    "data":{
        "username":"用户唯一的名称",
        "password":"密码",
        "phonenumber":"注册手机号码12位",
        "address":"邮箱地址"
    }
}
```

#### 响应内容

http 响应消息 body 中， 数据以json格式存储，

如果添加成功，返回如下

```json
{
    "status": 0,
    "id" : 677
}
```

ret 为 0 表示成功。

id 为 添加客户的id号。

如果添加失败，返回失败的原因，示例如下

```json
{
    "status": 1,    
    "msg": "客户名已经存在"
}
```

ret 不为 0 表示失败， msg字段描述添加失败的原因



### 上传文件（视频/图片）

#### 请求内容

请求消息

```
POST /video/upload
```

请求参数

```
data: {
    values: {
    	username: ‘用户名字’
    	filetype: 'image'/'video'(文件类型)
    },
    files: {
    	file: imgSrc
    }
}
```

#### 响应内容

响应参数

成功上传

```
{
	status: 0,
	filepath: '服务器端文件名称'
	
}
```

上传失败

```
{
	status: 0,
	"msg": "上传失败"
}
```



### 视频转换

使用facepy

请求消息

```
POST
/video/faceswap
```

请求参数

```
{
	username: 'username'
	imagepath: '图片路径'
	videopath: '视频路径'
	swapname:'swapname转换后文件名称(没有后缀)'
}
```



响应参数

成功开启任务

```
{
	status: 0
	task_id: 任务id
}
```

失败

```{
{
	status:1
	msg: 失败信息
}
```



### 查看转换进度

请求消息

```
POST
/video/view_task
```

请求参数

```
{
	username: 'username'
	task_id: '任务id'
}
```

#### 响应

正在转换

```
{
	'status': 0, 
	'progress': progress (任务进度)
}
```

转换结束

```
{
	'status': 1, 
	'progress': '转换结束'
}
```

转换出错

```
{
	'status': 2, 
	'progress': '错误信息'
}
```







### 下载视频

```python
from django.http import FileResponse
def download(request):
file=open('crm/models.py','rb')
response =FileResponse(file)
response['Content-Type']='application/octet-stream'
response['Content-Disposition']='attachment;filename="models.py"'
return response
```



stream流

```python
from django.http import StreamingHttpResponse
 
def big_file_download(request):
  # do something...
 
  def file_iterator(file_name, chunk_size=512):
    with open(file_name) as f:
      while True:
        c = f.read(chunk_size)
        if c:
          yield c
        else:
          break
 
  the_file_name = "big_file.pdf"
  response = StreamingHttpResponse(file_iterator(the_file_name))
  response['Content-Type'] = 'application/octet-stream'
  response['Content-Disposition'] = 'attachment;filename="{0}"'.format(the_file_name)
 
  return response
```



暂定方案

后端上传文件到静态路径

前端下载

请求url

```
服务器地址:端口号/static/media/username/文件名
```



### 会员充值

请求消息

```
POST
/common/modifytype
```

请求参数

```
{
	userid: 'userid'
	newtype: 2000
}
```

#### 响应充值成功

```
{
	'status': 0, 
}
```







### 视频展示

请求url

```
GET
服务器地址:端口号/video/test_resp/?path = /username/video.mp4

#示例：http://47.101.134.158:8888/video/test_resp/?path=/test/output.mp4
```



### TODO List

- [ ] 进度条
- [x] 换脸算法加速 - 效果并不好
- [x] 灰色按钮 
- [ ] 
- [ ] docker

# 服务器安装

- 系统：ubuntu

- 安装miniconda

```bash
wget -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-4.6.14-Linux-x86_64.sh
bash Miniconda3-4.6.14-Linux-x86_64.sh
```

- 环境安装

```
conda install opencv
pip install django
python -m django --version #查看版本

```

- 视觉处理库dlib安装
    - 下载安装包  http://blog.dlib.net/
    - 解压安装包，在根目录下执行`python setup.py install`

- 编译器插件安装

```
python
SQLite
```

- django设定

    - 在config文件中setting设置

    - ```
        ALLOWED_HOSTS = ['服务器地址']
        ```


- 视频编码器安装
    - 安装x264编码`sudo apt-get install x264 libx264-dev`
    - 安装ffmpeg `sudo apt-get install ffmpeg`
- redis安装

```
wget http://download.redis.io/releases/redis-6.0.8.tar.gz
tar xzf redis-6.0.8.tar.gz
cd redis-6.0.8
make
```

- 启动

- ```
    cd src
    ./redis-server
    ```

- 

# 报错问题解决

#### django的post请求403解决方法



Django默认开启防止csrf(跨站点请求伪造)攻击，在post请求时，没有上传 csrf字段，导致校验失败，报403错误

在settings.py里面的MIDDLEWARE_CLASSES中去掉“‘django.middleware.csrf.CsrfViewMiddleware’,”。



**安全解决方法：**

django的csrf安全工作顺序是：先从后台获取csrf_token 并发送给前端，然后前端在进行form表单提交时，把带有名为csrfmiddlewaretoken，值为 csrf_token 的字段一起发送给后端进行校验。

所以此解决方案便是按照此逻辑，先通过一个接口获取 csrf_token，然后在form表单中一起提交给后端校验

```javascript
from django.template.context_processors import csrf

def get_csrf(request):
        #生成 csrf 数据，发送给前端
    x = csrf(request)
    csrf_token = x['csrf_token']
    return HttpResponse('{} ; {}'.format(str(re), csrf_token))
```

然后在另一个POST请求中 加参数 名为：csrfmiddlewaretoken 值为 get_csrf函数返回的csrf_token ,这样校验便成功

优点：完成了 csrf 安全校验





#### 创建表后显示无table

```
python manage.py makemigrations --empty users
python manage.py makemigrations
python manage.py migrate users
python manage.py migrate
```



#### request.POST没有内容

原因：django没有对'Content-Type':'application/json'做处理

解决方法：在前端对content-Type进行修改

```
param.headers['Content-Type'] = 'application/x-www-form-urlencoded; charset=utf-8';
```



#### 静态文件路径访问404

在config中将setting修改为True

```
DEBUG = True
```



#### 安装dlib内存不足

解决方案：扩展SWAP

```
#获取要增加的2G的SWAP文件块
dd if=/dev/zero of=/swapfile bs=1k count=2048000
#创建SWAP文件
mkswap /swapfile 
#激活SWAP文件
swapon /swapfile   
#查看SWAP信息是否正确
swapon -s  
#添加到fstab文件中让系统引导时自动启动
echo "/var/swapfile swap swap defaults 0 0" >> /etc/fstab
```

编译完成后删除空间

```
swapoff /swapfile
rm -rf /swapfile
```



#### 较大的视频文件上传错误

网络问题

关闭vpn，保持网络畅通



#### 'DisabledBackend' object has no attribute '_get_task_meta_for'

```

```



# 算法加速

在detectorface的时候很消耗时间，考虑利用小位移去模拟跟踪。



# 测试报告模板

| 报告类型                                       | 报告内容 | 所处位置 | 下载版本 | 复现操作 |
| ---------------------------------------------- | -------- | -------- | -------- | -------- |
| 操作不足（无逻辑错误，但操作影响用户体验）     |          |          |          |          |
| 美观不足（无影响功能实现，但体验不足）         |          |          |          |          |
| 逻辑不足（逻辑不足，但运行得到目标结果）       |          |          |          |          |
| 逻辑警告（逻辑错误影响目标结果，但软件不崩溃） |          |          |          |          |
| 逻辑崩溃（逻辑错误导致软件崩溃）               |          |          |          |          |

