# Torchvision

## Torchvision.dataset.ImageFoler

Imagefolder是一个通用的数据加载器，他要求我们以下面的格式来组织数据集的训练、验证、以及测试图片

 

root/dog/001.png(jpg)

root/dog/002.png(jpg)

root/dog/003.png(jpg)

 

root/cat/001.png(jpg)

root/cat/002.png(jpg)

root/cat/003.png(jpg)

 

 Transform:对图片进行预处理的操作函数，原始图像作为输入，输出转换后的图片

loader：表示数据集的加载方式，通常默认加载方式

