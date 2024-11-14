每个a都是一个vector（向量），所有的a构成一个序列。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141900464.png)

如上图，感觉self-attention其实和全连接层差不多，但是self-attention的参数量比全连接层要小。

那么，如何得到每一个输出b呢？每一个b都是关联考虑了整个序列后得到的，所有要得知其它a与当前a的关联性。如下图：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141909597.png)

那要如何得到这个关联性呢？如下图，有两种方法。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141916086.png)

**Dot-product**（比较常见）

两个vector（也就是两个a）分别乘上不同的权重矩阵，得到新的q和k两个vector。然后将q和k进行点乘，得到的alpha是一个值，就是两个a的相关性参数（称为attention score，注意力分数）。

**Additive**

