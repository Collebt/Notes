# 图匹配综述（方便论文查找）

Given the feature points extracted from an image, we can construct a graph by associating each feature point to a node and specifying edges. This procedure naturally provides convenience to investigate the intrinsic structure of image data, especially for the matching problem. By this definition, graph matching (GM) refers to the establishment of node-to-node correspondences between two or multiple graphs. For its importance and fundamental challenge, GM

图匹配是一种长期有益的研究：

目前了解到的信息：

	- 在深度学习之前，图匹配是图像匹配的主流研究方向，有深厚的研究基础，并且是一个大坑
	- 图论应用于图像处理中可以脱离二维图形信息的范畴，考虑到更多连接关系
	- 目前Transformer的流行侧面说明后续网络连接数越来越多，能力会超越CNN，很具有潜力
	- 

## 图匹配问题

### 问题定义：



### 数学定义：

边缘相关度矩阵
$$
W_{i_1j_1,i_2,j_2} = exp(-\frac{(||X_{i_1i_2}||-||Y_{j_1j_2}||)^2}{2500})
$$


### 数据集：

生成数据集：

synthesized random point sets



真实数据集：

PASCAL

CMU House sequence

Motorbikes pairs

 

### 相关工作：

**SMAC:Balanced Graph Matching**

Cour, T., Srinivasan, P., Shi, J.: Balanced graph matching. In: NIPS (**2006**)

---

**GA: Graduated assignment**

S. Gold and A. Rangarajan, “A graduated assignment algorithm for graph matching,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 18, no. 4, pp.377–388, **1996**.

---

**SM:A spectral technique for correspondence problems using pair-wise constraints**

Leordeanu, M., Hebert, M.: A spectral technique for correspondence problems using pair-wise constraints. In: ICCV (**2005**)

---

**PM: Probabilistic graph and hypergraph matching**

Zass, R., Shashua, A.: Probabilistic graph and hypergraph matching. In: CVPR (**2008**)

---

**IPFP:An integer projected fixed point method for graph matching and map inference**

Leordeanu, M., Hebert, M., Sukthankar, R.: An integer projected fixed point method for graph matching and map inference. In: NIPS (**2009**)

---

**PRWM:Reweighted random walks for graph matching**

Cho, M., Lee, J., Lee, K.M.: Reweighted random walks for graph matching. In: ECCV (**2010**)

---

**FGM:Factorized graph matching**

Zhou, F., la Torre, F.D.: Factorized graph matching. IEEE Trans. Pattern Anal. Mach. Intell.38(9), 1774–1789 (**2016**)

---

**MPM：A max-pooling strategy for graph matching in the presence of outliers**

Cho, M., Sun, J., Duchenne, O., Ponce, J.: Finding matches in a haystack: A max-pooling strategy for graph matching in the presence of outliers. In: CVPR (**2014**)

---

**A dual decomposition approach to feature correspondence.**

Torresani, L., Kolmogorov, V., & Rother, C. (**2012**). A dual decomposition approach to feature correspondence. IEEE Transactions on Pattern Analysis and Machine Intelligence, 35(2), 259–271.

---

**A dual ascent framework for Lagrangean decomposition of combinatorial problems**

Swoboda, P., Kuske, J., & Savchynskyy, B. (**2017**). A dual ascent framework for Lagrangean decomposition of combinatorial problems.In Proceedings of the IEEE conference on computer vision and pattern recognition, pp. 1596–1606





### 研究方向：



有没有工作使用深度网络来优化随机游走网络的？

