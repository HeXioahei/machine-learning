是实现数据降维的一种算法，使得数据降维后损失的信息最少。

比如，给我们一个二维平面点的集合，这些点显然可以画在一个平面直角坐标系中，而pca要做的就是再找一个坐标系，使得这些点在新坐标系某轴线上的投影尽量不重合，这样就实现了化平面的二维为轴线的一维，且投影不重合就使得在变换的过程中能尽量保留更多的信息，且原数据点尽量保留自身原来的信息，也即最主要的信息。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410030009427.png)


怎么样才能找到这样的坐标系呢？投影尽量不重合，仔细看图想想，其实就是投影点在轴线上尽量分开，那么，它们的方差就会越大。所以，就是要使得轴线上的投影点方差最大，这个轴线就代表着主成分，也就是pca算法要寻找的目标。

那么，如何一步一步地找到这个新坐标系。

首先，中心化，也即去均值。把新坐标原点放在数据中心。

然后，找坐标系，旋转新坐标系，找到方差最大的方向。

最后，存储涉及到的信息：新坐标系的原点、新坐标系的旋转角度、新坐标点（也即投影点在新坐标系中的表示）。

这就需要线性代数来发挥大作用了。将数据用矩阵来表示，设为D，其左乘一些特殊的矩阵，其描绘的图形便可以实现一些奇妙的变换，比如左乘对角矩阵S可以实现拉伸，左乘协方差矩阵R可以实现旋转。
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410030008072.png)
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410030035993.png)



从上面的步骤我们可以知道，pca最重要的就是旋转找到新坐标系，那么其实就是求出协方差矩阵R。

我们得到的新坐标系相对于旧坐标系来看是旋转过的，是歪斜的。平的左乘R，旋转，得到斜的。那么，斜的左乘R$^{-1}$，逆旋转，变成平的。也就是说，我们手上的旧坐标系的数据点矩阵左乘R$^{-1}$便旋转得到新坐标系的数据点矩阵。

那么，怎么求R呢？

上面有提到，协方差矩阵就是R。什么是协方差？这是统计学里的一个概念，用来衡量变量之间的联合变化关系。计算公式如下：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/%E5%8D%8F%E6%96%B9%E5%B7%AE%E8%AE%A1%E7%AE%97%E5%85%AC%E5%BC%8F.png)

它可以表示两个变量是同向变化还是反向变化，同向和反向的程度如何。结果大于零，说明同向变化，即正相关。
协方差矩阵R如下（C就是R），为对称矩阵：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410030003747.png)

根据协方差计算公式可以看出，为什么要先取均值进行中心化后再旋转呢，就是为了使均值项为零，简化计算公式。

对于上面提到的白数据而言，两个变量之间没有相关性，故协方差为0，其协方差矩阵就为对角矩阵。

去均值后，根据计算公式可以进一步推导出协方差矩阵的计算公式为：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410030027115.png)
进一步推导出我们手上数据的协方差：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410030037117.png)
协方差的特征向量：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410031025794.png)        --->          ![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410031026517.png)     ---->![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410031027928.png)   --->   ![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410031028427.png)



R就是特征向量的组合结果，两个特征向量分别对应着新坐标系横轴和纵轴的方向。L由特征值组合而成，放映的是拉伸程度。

所以，新坐标系的基底就是协方差矩阵的特征向量，