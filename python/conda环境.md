# conda创建环境

`conda create -n env_name python=3.6`



使用yaml创建环境

`conda env create -f pytorch17.yaml`



yaml内容

 ```yaml
# environment.yaml

name:  env_name

channels:

    \# - https://dx-mirrors.sensetime.com/anaconda/cloud/python

    - pytorch
    - conda-forge
    - defaults

dependencies:

    - python=3.8

    - cudatoolkit=10.2

    - pytorch=1.8.0

    - pytorch-lightning<=1.1.8

    - pip

    - pip:

         -r [file:requirements.txt](file://requirements.txt)
 ```

​        

requirements.txt内容

```txt
opencv_python==4.4.0.46
albumentations==0.5.1 --no-binary=imagug,albumentations
ray>=1.0.1
```

## 用conda安装requirements.txt的内容

```
conda install --yes --file requirements.txt
```



## 用pip安装requirements.txt

```
pip install -r requirements.txt
```



## 复制环境

1. 拷贝想复制的环境文件夹到目标服务器的anacondas3/envs/NewName
2. 打开终端： `conda create -n NewName --clone ~/path(环境的位置)`



## 删除环境

```
conda remove --name ENV_NAME --all 
```



## Conda 安装gdal

gdal的安装比较困难，用常规方法还会报错。。

特此记录一下，主要是软件包的连接库要调一下

```
conda install -c conda-forge gdal #使用特定软件库下载

gdalinfo --version #查看是否安装成功
```



### 出现报错的解决方法

 *ImportError: libtbb.so.2: cannot open shared object file: No such file or directory*

```
conda config --set channel_priority strict
conda update -c conda-forge gdal
```



### python 导入

```
from osgeo import gdal
```





### conda 安装常用包

cv2

```
conda install -c conda-forge opencv
```

