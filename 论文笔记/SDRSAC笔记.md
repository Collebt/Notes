# SDRSAC：使用随机抽样的半正定规划求解点云匹配



## 将匹配问题转化成半正定规划问题



邻域矩阵的定义:
$$
\bold{A}= 
\left\{ %左括号 
\begin{array}{ccc} %该矩阵一共3列，每一列都居中放置 
f(\bold{p}_a, \bold{p}_c, \bold{q}_b, \bold{q}_d), & \text{if}|\delta(\bold{p}_a, \bold{p}_c)-\delta(\bold{q}_b,\bold{q}_d)|\leq\gamma\\
0, & \text{other}
\end{array} 
\right.  %右括号
$$

邻域矩阵$\bold{A}$定义了边的属性（二阶属性）


$p_i$表示的是image上关键点的坐标系$(x,y)$,



$X$定义了边上的属性（一阶属性）

$X\in R^{n \times n}$ 对应两张图中源图（source image）的$n$个点对应另一张目标图（target image）$n$个点的匹配可能性。



由此引出了目标函数：
$$
\max_\bold{X} \bold{X^\top A X }
$$

匹配问题中匹配对的特点：

- 一个点只能最多匹配上另一张图的另一个点
- 匹配对的数量不会超过一张图上的点数

由此得到约束：
$$
\bold{X1}_n\leq\bold{1}_m \\
\sum_{j=1}^{N} X_{i,j} \leq 1 \forall i,j \in \{1,\}
$$

