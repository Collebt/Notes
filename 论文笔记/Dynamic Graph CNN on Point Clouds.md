# 用于点云语义学习的动态图CNN



**任务类型**：对点云部位进行语义学习和分类



**希望的启发**：

- 如何得到点云聚类的方法：用卷积学习边的权重

- 监督信息是什么：已经分好类的点云



The model is capable of grouping points both in Euclidean space and in semantic space.



## Contributions

- EdgeConv, a novel operation for learning from point clouds to better capture local features of point clouds while still maintaining permutation invariance.
- semantically group points by dynamically updating a graph of relationships from layer to layer.



## Formulation

points: $X={x_1, x_2,...,x_n} \in \mathbb{R}^F$

e.g. $\bold {x}_i =(x_1, x_2, x_3)\in \mathbb{R}^3$ in Euclidean space



\