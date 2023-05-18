into

两类：基于类别的图像检索，基于内容的图像检索



一开始说明是”同一场景的检索“ 同一目标也行，要说清楚。

要说明太概要了，说具体一点，参考做检索目标的任务写intro



做这个任务的一段把两种方法的不足写完，参考光-SAR的方式只能解决模态问题，参考目标定位的工作只能解决目标问题



motivation 跟杨老师说一下能不能做geolocal，或者写第二点

1. geo-localization，
2. 大的对齐，然后像素对齐。写得宽泛一点的任务的前置任务。:heavy_check_mark:





related

第一段多说一些，检索是干嘛的，同一模态、同一目标的检索、同一类别。要总结清楚他们的不足。

三段的行文就删掉，

在method上介绍

1. 任务的难点问题、2. “对抗学习的工作机理”，能够解决这个问题。对症下药。

例子：我们的任务抽象出这个具体问题， gnn能够解决具体问题，然后用gnn解决这个具体问题。





method

A.overview 变短一点， :heavy_check_mark:

C.要强调一下是光的gps，为什么不用SAR的gps（没有或不准）

提出要假设以及对应的实验验证。

D.强调end-to-end 的训练过程和不需要分开训练。





experiment 分析太少了

总分总：

1. 我们方法最好

2. 哪一类的方法不行，不行的原因

3. 我们的方法这么做的，考虑到了什么问题，效果好。





visual

可视化结果并不好，就不加了





dataset

数据集的具体操作和构建 :heavy_check_mark:

目前还没有还没有人做做过大规模的数据集，所以还没有这个任务，我们构建这个数据集。



metric就少写一些。







---

所有图字体的格式， 大小要统一



数据图对齐:heavy_check_mark:



frame图的元素均衡一点, 改成另一个图 :heavy_check_mark:

fig. 2: shared weights， 叠在中间。  :heavy_check_mark:

fig.3： 对齐 :heavy_check_mark:



grided vs. :heavy_check_mark:





dis: 数据量的原因，导致预测效果变差， limitation。feature work： 数据库运营。

讨论光-SAR能不能做？视角还是比较理想化的，考虑真实场景的应用，本文只是原理上的设计，下一步使用移动终端，手机探索匹配定位。

尽管用的数据是人工进行矫正的，下一步探究倾斜的情况下（真实）

提及移动终端的视野很小（patch小）。







---

experiments:

1. benckmask
   1. introduce method :heavy_check_mark:
   2. method comparison:heavy_check_mark:
   3. visualizae analysis:heavy_check_mark:



2. ablation
   1. module analysis:heavy_check_mark:
   2. adversarial analysis :heavy_check_mark:
   3. gnn analysis:heavy_check_mark:

discussion:

1. wassersetin learning :heavy_check_mark:
2. gnn:heavy_check_mark:
3. limitation and future work:heavy_check_mark:



