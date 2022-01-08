# Joint Cuts and Matching of Partitions in One Graph

pdf:  [Yu et al-2017-Joint Cuts and Matching of Partitions in One Graph.pdf](..\..\ZoteroFiles\Graph Matching\Yu et al-2017-Joint Cuts and Matching of Partitions in One Graph.pdf) 

文章主要是通过

 [GCN近似.md](GCN近似.md) 



graph cut problem
$$
\min _y \frac{y^TL^gy}{y^Ty}
$$


文章首先提出了将graph cat和graph matching联合在一起的解法。

首先定了了联合了两个问题的目标方程，然后用梯度下降的方法求解问题

目的是为了更新matching的X， 

1. compute the partial iderivative of E
2. 
