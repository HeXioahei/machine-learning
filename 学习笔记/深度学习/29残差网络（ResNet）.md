> 课程：李沐《动手学深度学习》
> 课程视频：[29 残差网络 ResNet【动手学深度学习v2】_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1bV41177ap/?spm_id_from=333.1007.top_right_bar_window_history.content.click&vd_source=327f3e87e497fe83b3515199232efd15)

*代码实现：[machine-learning/代码实现/ResNet.ipynb at master · HeXioahei/machine-learning (github.com)](https://github.com/HeXioahei/machine-learning/blob/master/%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0/ResNet.ipynb)*

# 意义用途
我们总是企图加深神经网络来得到更精确的结果，但是加深不一定总能带来好处。随着网络的不断加深，函数的复杂度不断增大，其覆盖的范围不断扩大，但是，它不受控制，它扩大的方向可能并不是接近最优值的方向。

比如，假设我们所要寻找的最优值其实就在我们目前函数覆盖范围的上方，但是我神经网络的加深却是往下方不断加深的，这就逐渐偏离了正确方向。不断地加深反而越来越差。

如何**使得加深不会偏离最优值**。ResNet就给出了解决思路，即每一次加深都要求在**原来函数的基础上进行扩充**，新得到的函数必须包含原函数，就像是水中的涟漪不断从中心扩大，这样的话各个方向都可以被搜寻，就不会偏离，模型就不会随着网络的加深而变差。

所以，ResNet的核心思想就是，加更多的层时，不会使模型逐渐变差，不会偏离最优解。

# 实现方法

## ResNet块
其与普通卷积神经网络的对比如下：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410050935632.png)

*图有误，`f(x)`应改为`g(x)`*

左边是普通卷积神经网络；右边是ResNet块，概括来说就是`f(x)=x+g(x)`这样的一个结构。虚线方框里的部分其实就相当于`g(x)`，即使我们不做`g(x)`部分的处理，或者说`g(x)`部分的学习成果几乎为零，那也存在着`x`部分的继承，使得新得到的函数至少等于原函数`x`。若`g(x)`部分有作用，那么就是在原函数的基础上再加上一部分，即学到了一部分新东西。

ResNet细节如下：

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410050953693.png)

由是否含有‘1×1卷积层’分为两种实现。

**为什么加入一个1×1的卷积层呢？**

`x`在经过`g(x)`层的变换后，它的输出通道数与`x`原本的输出通道数可能是不一样的，不一样的话就无法和原来的`x`进行相加，就无法得到`f(x)`。所以，‘1×1卷积层’的作用就是变换通道数。

## 不同的残差块

三个层——卷积层、批量规范化层、激活函数层，`x`可以随意插入到任意层之间，这样就可以产生不同的残差块，理论上来说这些组合都是合理的，只是要根据具体需求来看是否有实际便利作用。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051022201.png)


## ResNet块基本组合

先是通过步幅为2的卷积层，将输入的矩阵的高宽减半。后面接多个步幅为1的ResNet块，使高宽保持不变，重复多次进行学习。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410052331149.png)

## ResNet架构

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410052333668.png)

与VGG和GoogleNet的总体架构类似，但替换成了ResNet块。

# 总结
* 残差块使得很深的网络更加容易练习，甚至可以达到1000层。
* 残差网络对随后的深层神经网络设计产生了深远的影响，无论是卷积类网络还是全连接类网络。
* 但是，残差网络也使得模型的复杂性增加了。


