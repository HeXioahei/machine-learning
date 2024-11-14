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
2. 所有a的Wq、Wk、Wv都是一样的。

所有的b都是并行同时计算出来的。