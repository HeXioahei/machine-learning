[BN层详解-CSDN博客](https://blog.csdn.net/qq_38900441/article/details/106047525?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ECtr-1-106047525-blog-112853861.235%5Ev43%5Epc_blog_bottom_relevance_base5&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ECtr-1-106047525-blog-112853861.235%5Ev43%5Epc_blog_bottom_relevance_base5&utm_relevant_index=2)
[BN(Batch Normalization)层原理与作用_bn层的原理和作用-CSDN博客](https://blog.csdn.net/chaipp0607/article/details/112853861)
[Batch Normalization详解以及pytorch实验_pytorch batch normalization-CSDN博客](https://blog.csdn.net/qq_37541097/article/details/104434557)

我们在图像预处理过程中通常会对图像进行标准化处理，这样能够加速网络的收敛。对于第一层卷积来说，输入的是数据集整体满足分布规律的特征矩阵，而对于第二层卷积来说，输入的是经过第一层卷积后的特征矩阵，其整体不一定再满足一定的分布规律。我们要对整个图像数据集进行标准化处理，那就要求整个图像数据集的特征图的均值为0，方差为1。可是，整个数据集超大的，最真个数据集进行这种标准化处理显然是不可能的。因此，我们可以用batch normalization。

batch就是批次，可以理解为，每次对单批次的数据进行标准化处理，得到该批次的均值和方差，并将其保留下来，等其他批次的标准化操作都做完都得到相应的均值和方差之后，再进行统计。统计的结果即可认为是整个数据集的均值和方差。然后在我们的验证和预测过程中，就可以用这个统计的均值和方差来进行标准化处理。

*我的理解是，这个统计均值和方差的过程是否也可以理解为是一种学习的过程，通过不断的数据输入计算均值方差，统计结果会不断地更新，就相当于是在学习，然后得到最合适的最近似整个数据集均值方差的均值方差。这个过程是在训练中进行的，得到的统计结果，也即训练学习的结果，就被应用在后续的验证和预测过程中，用来进行标准化处理。*

*怎么进行标准化处理？可以回顾之前PCA的内容，原理类似。得到数据的均值和方差后，即可进行标准化处理。*

以上斜体部分的理解应该是错的，BN里有两个参数 $\gamma$ 和 $\beta$ ，是可学习的参数，在反向传播过程中不断更新。$\gamma$ 是用来调整数值分布的方差大小， $\beta$ 是用来调节数值均值的位置。这两个参数是在反向传播过程中学习得到的，$\gamma$ 的默认值是1， $\beta$ 的默认值是0。

好吧，还是不太懂。