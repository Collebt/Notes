# Learning Combinatorial Solver for Graph Matching



2020 CVPR

## assign graph 
在生成分配图assignment graph 时,输入的是一个btach的Tensor,如何对进行并行操作?



在`dataloader`中`__get_item__`获得

有没有方法使用矩阵的乘法获得?


$$
G^A_{ij} = G^1_{ij} * G^2_{ab}
$$
For edge generation of $G^A$ , we build an edge between a pair of nodes $v_{ia}^A, v_jb^A$,
nodes $v_{ia},  v_{jb}∈  V^A $if and only if there are two edges $(v i , v j ) ∈ E (1) $and$ (v_a , v_b ) \in E^(2)$ .



对于图邻域矩阵A的分解得到$G,H \in R ^{N_v \times N_e}$ , 其中$N_v$为节点的数量. $N_e$为边的数量. 重构A为$A = GH^T$

![image-20210414155543825](image-20210414155543825.png)

F in (b)



#### GMN的`reshape_dege_feature()`函数输入参数

~~最后一个维度的数据是一样的,都是egde_num,~~

将输入的F特征映射为边特征(线性映射,不参与学习)

```
F.shape = (batch_num, feat_num, node_num)
G,H.shape = (batch_num. node_num, edge_num)
X.shape = (batch_num, 2*feat_num, edge_num)
X[:, 0:feat_dim, :] = torch.matmul(F, G) 
X[:, feat_dim:2*feat_dim, :] = torch.matmul(F, H)
```



