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

