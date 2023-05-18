# graph matching via spiking neural network



在图匹配问题中，匹配环节一直存在没有解决的问题：如何对语义上一致的节点进行匹配？除了sinkhorn之外，目前还没有很好的方法可以解决1. 梯度连续， 算法可解释性， 匹配策略泛化性的问题，



1）sinkhorn是hangrian的梯度近似版本，但是对于匹配结果的0-1分布，sinkhgorn难以实现0-1的结果输出， 而传统的hungraian算法则无法反传梯度，导致网络无法学习。



2） sinkhorn的灵活性较差，当图匹配中存在outlier的情况（size-varied）， 无法得到一种可以筛选outlier的策略。



3）sinkhorn需要迭代才能计算出结果，并且匹配环节中没有可学习的参数，当节点embedding较差的时候，该匹配策略效果会急剧恶化，因此深度图匹配中，当前的工作难以在匹配环节加入深度网络的效果。导致泛化性较差。





针对这三个问题，我们应该找一种能够满足输出为0-1分布的匹配策略，并且其中具有可学习参数，对应目前的匹配环节是无监督策略，我们不需要设计的方法具有很好的梯度性质，也不需要大数据进行学习和拟合，而是能够具有一定的自监督功能，一定的逻辑推理能力。



目前来看，SNN比较适合，因为snn加入了脉冲，脉冲的性质能够很好地匹配到输入0-1分布的需求。



而且该方法不需要大数据进行监督训练，可以通过自监督的方式进行参数更新。



> SNNs have increased productivity of information processing and noise immunity since they use the temporal presentation of information.



