# nerf的相关论文和综述

nerf[^1]用mlp隐式表达了三维场景的几何和texture信息用MLP的权重表达，输入为任意的空间坐标和观察角度，输出为在该观察角度下每一个体素的rgb颜色和体密度，再通过积分到二位平面上得到三维场景的图像。



1. nerf每一次训练的模型只能表达一个场景，优化时间长

2. pre-pixel渲染低效（什么是pre-pixel）
3. 泛化能力差，每一个场景需要较多图片才能训练好。



针对训练时间长的问题，nvidia的基于哈希编码的nerf[^2]可以加速训练，只需要5秒。

Instant Neural Graphics Primitives with a Multiresolution Hash Encodin



针对需要多张图片，MINE[^3]结合了深度表示和nerf思想的模型，输入仅为单张图片和任意深度，用encoder输出图像feature map, 通过输入不同深度值到decoder和featuremap，得到N个不同深度的图像表示，以此得到连续三维场景图。他在思想上参考了nerf用mlp隐式表达三维场景的想法，用decoder隐式表达了在给定图像中的深度三维图。



同时由于nerf是基于优化的方法，每个场景需要单独优化，场景间没有共享只是，不仅耗时，而且无法利用先验知识来加速重建，在单个或稀疏视图的情况下效果很差。





















[^1]: NeRF: Representing Scenes as Neural Radiance Fields for View Synthesis
[^2]: Instant Neural Graphics Primitives with a Multiresolution Hash Encoding
[^3]: MINE: Towards Continuous Depth MPI with NeRF for Novel View Synthesis

