# Self-Attention
每个a都是一个vector（向量），所有的a构成一个序列。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411141900464.png)

如上图，感觉self-attention其实和全连接层差不多，但是self-attention的参数量比全连接层要小。

那么，如何得到每一个输出b呢？每一个b都是关联考虑了整个序列后得到的（为什么要关联考虑整个序列呢？比如，一个英文句子里同时出现两个一样的单词，但是它们的词性不一样，一个是动词，一个是名词，这时，就需要考虑整个序列（也即整个英文句子）才能较准确地判断每个单词各自的意思），所以要得知其它a与当前a的关联性。如下图：

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

W只关心矩阵a的宽度，因为W的高度要和a的宽度相同才能进行矩阵乘法运算。那么，W的宽度要如何决定呢？W的宽度将决定最终每个向量q（或k、v）的长度，也就是矩阵q（或k、v）的高度，在多头注意力机制中可能还将影响头的数量。目前我还不知道W的宽度如何决定。

还有一些教程可能是如下表示的，其实都是一样的，只不过转置了一下，所以W放到后面去了，相应的，a也由横着堆叠变为竖着堆叠了。W仍然只关心向量a的长度，而不关心向量a的数量。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411142027284.png)


那么，还有个问题，一直感觉它和全连接十分相似啊，但又听说参数量好像减少了，具体是怎么回事呢？我感觉参数量好像没什么变化，毕竟有些代码实现里关于self-attention的实现就主要是用线性全连接层Linear来实现的。保留这个问题，看看后面会不会解决吧。

我们继续往下。

得到每个向量q和向量k之后，是要将他们相互进行点乘的。那么，一个个的向量点乘，其实也可以整合成矩阵的点乘。如下所示：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411142051815.png)


这样，就可以直接得到注意力分数矩阵了。在soft-max层里，其实还有对q和k点乘的结果做一个缩放。具体公式如下：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411142100857.png)

其中，dk就是向量q和k的长度。

然后，再和矩阵v进行点乘。如下：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411142056589.png)

细节，矩阵v要放在前面，这样才能保证列与行的对应。

整合全部过程，概括如下：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411142104426.png)

# Multi-head Self-Attention
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411142127996.png)

多头注意力机制其实和单头的区别不是很大，其主要是对每一个向量q、k、v再进行了进一步的划分。如q，通过乘以矩阵Wq1和Wq2分别得到向量qi1和qi2。然后1的和1的做运算，2的和2的做运算，也就对应着两个head，这样，对于每个向量a，就可以得到两个输出向量b（bi1和bi2）。如下：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411142132019.png)

然后再通过一个矩阵Wo来将二者合为一个输出向量bi。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411142133036.png)

# Position Encoding（位置编码）
学到这我们可以发现，self-attention并不关心位置，里面都没有位置信息。但是，有时，单个序列中每个输入数据的位置信息对于输出来说也是至关重要的。比如，一句英文句子就是一个序列，每个单词就是序列中的一个向量。我们可以通过通过单词的位置来判断它的词性，比如动词一般就不会出现在第一个位置。

所以，我们要做的就是在ai生成qi之前，给它加上一个位置编码ei。