## GNN分类

图卷积网络（GCN）

图注意力网络（GAT）

图空域网络（STN）

图自编码（Auto-GarphEncoder）

图生成网络（GN）



目标： 学习得到一个状态的嵌入向量（embedding） $hv \in R^5$ 

$hv$:节点$v$的状态向量，用于输出$Ov$（节点的标签）  ——特征向量



## cos距离

$$
cos(A,B) =\frac{A \cdot B}{||A||_2 ||B||_2} \\
||A-B||_{cos} = 1 - cos(A,B)
$$

 在归一化后 $||A||_2 = ||B||_2 = 1$
