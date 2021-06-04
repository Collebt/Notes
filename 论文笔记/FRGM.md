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

3. 如果仅仅是使用了内积去度量特征的相似性,就失去了图的结构化信息:

    由于没有使用到边缘的信息，这时需要用到边缘矩阵$\bold{E}$定义边的关系
    $$
    \mathbb{F}_\mathcal{V}: \mathcal{F}(\mathcal{V},\mathbb{R}) \times\mathcal{F}(\mathcal{V},\mathbb{R})  \to \mathbb{R}
    $$

令其满足$\mathbb{F}_\mathcal{V}(\phi_{i1}, \phi_{i2}) = \bold{E}_{i_1i_2}$



3. 函数空间$\mathcal{F}(\mathcal{V},\mathbb{R})$的内积可以隐式通过泛函数$\mathbb{F}_\mathcal{V}$表示:

$$
\mathbb{F}_\mathcal{V}(\phi_\bold{a}, \phi_\bold{b}) \triangleq \sum_{i_1, i_2} a_{i_1}b_{i_2} \mathbb{F}_\mathcal{V}(\phi_{i_1}, \phi_{i_2})=\sum_{i_1,i_2}a_{i_1} b_{i_2} \bold{E}_{i_1,i_2}
$$

如果只是内积,$\left<\phi_\bold{a}, \phi_\bold{b} \right> = \sum\limits_i a_ib_i$,相当于$\bold{E}_{i_1,i_2}$是全1的矩阵,相当于是全连接图,每一个边的权重都为1,那样就失去了图像的信息.

### 主要贡献

将图的结构信息用泛函表示:

用$\mathcal{F}(\mathcal{V},\mathbb{R}) $表示在函数空间中,对函数$\mathcal{V}$映射到实数空间$\mathbb{R}$. 



## 一些问题的解答

- 术语的解释

首先解释函数: 将有限维特征$x \in \mathbb{R}^n$作为输入,并映射到实数轴 ￼ （一维线性空间）或者复平面。微积分学（包括复变函数论、实变函数论）对“函数”进行了透彻的研究。

线性泛函分析：研究的是**无限维**线性空间和线性映射。如果一个线性映射，将无限维空间中的元素映射到实数轴 ￼（复平面也可），则称为“线性泛函”

- 泛函和函数、算子比较:

简单来说，算子是一个函数到另一个函数的映射，它是从**向量空间到向量空间的映射**，泛函是从**向量空间到数域的映射**，函数是从**数域到数域的映射**



- 线性泛函分析这门学科的目的就是：

1. 试图将线性代数的相关理论类比推广到无限维空间中去。在这方面最重要的结果就是Hahn-Banach定理和Riesz表示定理。

2. 由于无限维空间有界集不再是列紧集，“紧性”在分析学中是极其重要的。因此有必要研究无限维线性空间的拓扑，为此需要引入弱收敛、弱 * 收敛等概念。

3. 分析学研究空间与映射。因此除了在无限维空间引入不同的拓扑之外，线性泛函分析需要研究线性映射的性质。当然这里的线性映射不再局限于线性代数的有限维空间上的映射。这方面最重要的结果集中在Baire纲定理的一系列结果。

