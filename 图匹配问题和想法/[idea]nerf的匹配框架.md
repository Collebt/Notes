# 基于nerf的匹配框架

最近看nerf的文章，发现nerf的insight很动人。使用MLP去编码单一场景中的信息，而不是基于大数据进行embedding。这种模型的好处是对单一场景特异信息有更好的编码，缺点是没办法学习到数据分布中的信息。



针对匹配问题，特别是语义匹配，当特征的语义已经有比较好的embbeding的时候，更加需要着重于solver的设计