每个a都是一个vector（向量），所有的a构成一个序列。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141900464.png)

如上图，感觉self-attention其实和全连接层差不多，但是self-attention的参数量比全连接层要小。

那么，如何得到每一个输出b呢？每一个b都是关联考虑了整个序列后得到的，所有要得知其它a与当前a的关联性。如下图：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141909597.png)

那要如何得到这个关联性呢？如下图，有两种方法。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141916086.png)

**Dot-product**（比较常见）

两个vector（也就是两个a）分别乘上不同的权重矩阵，得到新的q（query）和k（key）两个vector。然后将q和k进行点乘，得到的alpha是一个值，就是两个a的相关性参数（称为attention score，注意力分数）。具体流程如下：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141926451.png)

a1拿着它的q去“查询”每一个a的k并进行“关联计算”（即dot-product）（包括查询关联自己的k）。其实soft-max这个地方可以替换成其他东西，其本质只想实现非线性罢了，我们也可以用relu。但是，soft-max可以实现归一化，使每个分数加起来为1。

再接下来，如下图：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141935151.png)

每个a都生成一个v（value）向量，再与前面得到的alpha‘（即注意力分数）进行相乘，再相加，得到当前a的输出b。

**需要注意的是**：

1. 并不是说离当前a越近的a得到的注意力分数就越大，它们的关联性不是只取决于它们在序列中的位置关系。
2. 所有a的Wq、Wk、Wv都是一样的，它们是可学习训练的参数。

所有的b都是并行同时计算出来的。具体的做法是将所有的vector拼接成一个矩阵，用矩阵乘法来统一解决。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141954601.png)

看到这里，我一直在想，所以到底为什么说这样就可以解决序列长度不一的问题呢？我的理解是这样的，不管每次序列里有几个向量（即有几个向量a），比如第一次有4个向量a，就构成了宽度为4的矩阵，如果第二次有7个向量a，它就是构成了宽度为7的矩阵，而权重矩阵放在前面，其和矩阵a做矩阵乘法，是不关心矩阵a有多宽的，只关心矩阵a有多高。所以，其实关键在于矩阵a的高度，也就是每个向量a的长度。也确实，既然向量a都可以拼接在一起，那么它们的长度肯定是有事先规定好的，事先预处理好的。比如，词嵌入处理，在进入self-attention层之前，先通过了词嵌入层，得到了统一规格的向量a，然后才进行self-attention的计算。

还有一些教程可能是如下表示的，其实都是一样的，只不过转置了一下，所以W放到后面去了，相应的，a也由横着堆叠变为竖着堆叠了。W仍然只关心向量a的长度，而不关心向量a的数量。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411142027284.png)


那么，还有个问题，一直感觉它和全连接层没什么区别啊，但参数量好像减少了，具体是怎么回事呢？

