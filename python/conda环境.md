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

1. 拷贝环境到anacondas3/envs
2. 打开 `conda create -n NewName --clone ~/path(环境的位置)`