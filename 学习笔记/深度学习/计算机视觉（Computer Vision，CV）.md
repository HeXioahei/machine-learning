# CV概述
## CV解决的问题
* 图片分类（Image Classification）
* 目标检测（Object Detection）
* 图片风格迁移（Neural Style Transfer）

## 卷积在处理大图像上的作用
对于一张64×64像素大小的图像，他的数据有64×64×3=12288个（3指的是颜色通道数，RGB三个）。这如果直接用全连接层来处理的话，尚且还能处理得了。

但是如果图片变大，比如1000×1000像素大小，那么，输入数据就有3m个（1m=1000,000），是一个(1, 3m)的矩阵。假设隐藏神经元只有1000个，那么，输入层与隐藏层之间得权重矩阵 w 就是维度为(3m, 1000)大小的矩阵，有3m×1000=3b（1b=1000,000,000）个参数，这是一个很大的数量级，会占用很大的内存。

所以，我们就需要用到卷积来处理大图像。

# 边缘检测
边缘检测可以用来识别物体，有垂直边缘检测、水平边缘检测等

例如，一张图片如下：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410111615584.png)

* 垂直边缘检测
	![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410111616417.png)
* 水平边缘检测
	![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410111617931.png)

## 如何进行边缘检测呢
例如，对于一张6×6的灰度图片，因为它是灰度图片，所以颜色通道数为1，所以，它是一个64×64×1的矩阵。如下图所示：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410111622075.png)（图像矩阵）

为了进行图像边缘检测，我们可以构造一个3×3的矩阵，习惯上，我们把它称为过滤器（filter）或者是核（kernel）（也即常说的“卷积核”）。对于垂直边缘检测，我们把卷积核构造如下：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410111626240.png)（核矩阵）

可以明显地看出，这个和矩阵的数据分布很具备垂直特征，因此，它可以很好的提取图像的垂直特征，具体怎么提取呢？我们接着往下。

我们对图像矩阵和核矩阵进行卷积运算（Convolution Operation），该运算可以用符号`“*”`表示。根据卷积运算规则：新宽 = （原宽 + 填充×2 - 卷积核边长）/ 步长 + 1，最终将得到一个4×4的矩阵，即4×4的图像。计算过程大致如下：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410111634994.png)

依次类推，移动蓝色方块，不断计算出4×4矩阵中所有的值。结果如下：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410111636994.png)

