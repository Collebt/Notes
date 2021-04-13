# TNT（TrackletNet Tracker）

![在这里插入图片描述](../20191219192316678.png)



**核心部分：**图模型（传统），将输入的节点和边权重进行聚类

节点生成：使用FaceNet

边权重生成：使用TrackletNet计算相似度$p_e$，计算相似度$c$
$$
c = ln(\frac{1-p_e}{p_e})
$$
<img src="../image-20210302110405074.png" alt="image-20210302110405074" style="zoom: 25%;" />

TrackNet相似度网络结构如下：

![image-20210302110500079](../image-20210302110500079.png)

