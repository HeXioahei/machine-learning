> 课程：李沐《动手学深度学习》
# 从全连接到卷积
## 分类猫和狗的图片
使用一个还不错的相机采集图片（12M像素） （1M=1000,000）。则RGB图片有36M个元素。使用100大小的单隐藏层MLP，则模型有3.6B个元素（1B=1000,000,000）。这远多于世界上所有猫和狗的总数。

3.6B个参数，大概需要14GB的储存空间。

## 两个原则
* 平移不变性：识别效果不会因为目标像素位置的改变而发生改变。不管在哪里都可以识别。
* 局部性：识别目标时，不需要观察整个图片，只需观察目标周围的部分便可以识别出目标。

## 重新考察全连接层
全连接层将一维的输入和输出变形为矩阵（矩阵具有宽度和高度，是二维的），而权重要把输入和输出联系起来，所以它与输入数据在输入矩阵中的位置和输出数据在输出矩阵中的位置都有关系，而输入和输出现在都是二维的矩阵，都由两个变量（行位和列位）来决定位置，所以相应的，权重就与四个变量有关，所以权重变成了一个四维的张量（从输入(h,w)到输出(h',w')）。
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062232473.png)

## 两个原则的实现
* ![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062231639.png)
* ![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062231242.png)
## 总结
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062236871.png)

# 卷积层
## 二维交叉相关
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062236469.png)

## 二维卷积层
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062245751.png)

## 交叉相关vs卷积
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062248601.png)

## 一维和三维交叉相关
* 一维：文本、语言、时序序列
* 二维：图片
* 三维：视频、医学图像、气象地图

---
> 课程：b站吴恩达深度学习课程
> [112.1.5 卷积步长_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV11H4y1F7uH?p=109&vd_source=327f3e87e497fe83b3515199232efd15)
