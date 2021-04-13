## 图映射到泛函空间

FUnctional Resresentation for Graph Matching



图匹配问题定义形式1：
$$
\max_{\bold{P}} vec(\bold{P})^\top \bold{K} vec(\bold{P})
$$
等价形式2：
$$
\max_{\bold{P}\in \mathcal{P}} \sum_{ij} \bold{P}_{ij}\bold{K}_{ij} + \sum_{i1,j1;j1,j2}\bold{P}_{i1j1}\bold{K}_{i1j1;i2j2}\bold{P}_{i2j2}
$$
表示成矩阵形式：
$$
\max_\bold{X} = \text{tr}(\bold{K}^\top \bold{P})+ \lambda \text{tr}( \mathcal{E}_1 \bold{P} \mathcal{E}_2 \bold{P}^\top)
$$
$\bold{K} = \mathcal{E}_1 \otimes \mathcal{E}_2$

这类问题求解的$X\in \{0,1\}^n$， 为匹配对存在的可能性，一般会松弛化为$0\leq X_{ij} \leq 1$。

松弛：
$$
\min_{\bold{P} \in \mathcal{P}} \left<\bold{P}, \bold{U} \right>_F + \frac\lambda 2 \|\mathcal{E}_1 - \bold{P} \mathcal{E}_1 \bold{P}^\top\|^2_F
$$
这是公式（3）的另一种等价情况：当$\bold{P} \in \mathcal{P}$是正交矩阵的时候，公式（3）和（4）等价。



### 定义和定理

1. **定义函数空间$\mathcal{F}(\mathcal{V, \mathbb{R}})$**

$$
\mathcal{F}(\mathcal{V, \mathbb{R}}) \triangleq \{\phi_a = \sum_i a_i\phi_i, \bold{a}\triangleq(a_1,a_2,...,a_m)^\top \in \mathbb{R}^m\}
$$

- 定义了内积：$\left<\phi_\bold{a}, \phi_\bold{b} \right> = \sum\limits_i a_ib_i$

- 度量：$d\left(\phi_\bold{a}, \phi_\bold{b} \right) = \sqrt{\sum_i(a_i-b_i)^2}$

 

2. **定义函数空间的函数$\mathbb{F}_\mathcal{V}$**

    由于没有使用到边缘的信息，这时需要用到边缘矩阵$\bold{E}$定义边的关系
    $$
    \mathbb{F}_\mathcal{V}: \mathcal{F}(\mathcal{V},\mathbb{R}) \times\mathcal{F}(\mathcal{V},\mathbb{R})  \to \mathbb{R}
    $$

令其满足$\mathbb{F}_\mathcal{V}(\phi_{i1}, \phi_{i2}) = \bold{E}_{i_1i_2}$



3. 函数空间$\mathcal{F}(\mathcal{V},\mathbb{R})$的内积可以隐式通过泛函数$\mathbb{F}_\mathcal{V}$表示:

$$
\mathbb{F}_\mathcal{V}(\phi_\bold{a}, \phi_\bold{b}) \triangleq \sum_{i_1, i_2} a_{i_1}b_{i_2} \mathbb{F}_\mathcal{V}(\phi_{i_1}, \phi_{i_2})=\sum_{i_1,i_2}a_{i_1} b_{i_2} \bold{E}_{i_1,i_2}
$$



### 推论

