# 用于凸函数的迭代求解极值



用于求解线性约束问题的算法，称为近似线性化方法。

基本思想：将目标函数线性近似，求解线性规划求得可行下降方向，并沿该方向做一维搜索（最小值）。



## Formulation

$$
\begin{array}{c}
 \min f(x) \\
s.t. Ax = b\\
x \geq 0

\end{array}
$$

其中$A \in R^{m \times n}$行满秩矩阵，$b \in R^m$， $f:R^n \to R$为可微函数，可行域为
$$
S = \{x|Ax = b, x\geq 0\}
$$


 近似线性化(线性化最有方向)
$$
f(x) \approx f(x_k) + \nabla f(x)^\top (x-x_k)\\
\Downarrow \\
\left\{ min f(x_k) + \nabla f(x_k)^\top (x-x_k) \atop
  s.t.   \space\space x \in S \\\right.
\Downarrow \\
\left\{  \min \nabla f(x_k)^\top (x-x_k) \atop
  \text{s.t.} \space\space x \in S  \right.
$$
当$\nabla f(x_k)^T (y_k -x_k) = 0$时，$x_k$是问题的K-T点；

当$\nabla f(x_k)^T (y_k -x_k) \not= 0$师，向量$d_k = y_k -x_k$是$f$在$x_k$处的可行下降方向



确定一维搜索步长
$$
\min_{0 \leq \lambda\leq 1}f(x_k + \lambda d_k)
$$


## 算法步骤

1. 选取初始数据，选取可行点$x_0$，允许误差$\epsilon\leq 0 ，k=0$

2. 求解近似线性规划最优解$y_k$
    $$
    \left\{  \min \nabla f(x_k)^\top (x-x_k) \atop
      \text{s.t.} \space\space x \in S  \right.
    $$

3. 构造可行下降方向$d_k = y_k -x_k$，求解$\min_{0 \leq \lambda\leq 1}f(x_k + \lambda d_k)$,获得最优解$\lambda_k$，转2
4. 当误差$||\nabla f(x_k)^Td_k|| \leq\epsilon $时，停止迭代。



## 结论：

Frank-Wolfe算法是一种可行方向法，在每次迭代内，搜索方向总是指向某个极点，并且当迭代点接近最优解时，搜索方向与目标函数的梯度趋于正交，因此算法收敛速度比较慢.但该方法把求解非线性最优化问题转化为为求解一系列线性规划问题，而且各线性规划具有相同的约束条件，因而该方法在实际应用中仍然是一种有用的算法．
------------------------------------------------
版权声明：本文为CSDN博主「gnefniu」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/gnefniu/article/details/17529609