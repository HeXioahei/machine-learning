> 课程：李沐《动手学深度学习》and  哔哩哔哩up主“FunInCode”【数之道】系列视频
# 感知机
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051033538.png)
先取内积，在加上偏移量，再放入一个函数中，最终只有两个结果。可见，他是一个二分类问题（不一定是1和0，也可以是1和-1）
## 训练感知机
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051041419.png)

$y_i$ 是标签值，$<w,x_i>+b$  是预测值，分类正确的话就是负负得正或者正正得正，如果这两个相乘≤0，则说明该预测分类是错误的，那么就要改变权重**w**和偏移量**b**了。一直这样检测下去，直到所有的分类都是正确的。

下面那个损失函数更准确来说应该为  $l(y,x,w)=max(0,-y(<w,x>+b))$ 。当分类正确时，$-y(<w,x>+b)$ <0，$l$ 就等于0。也就是，分类正确，无需调整，损失为零。

## 收敛定理
假设所有的数据在半径`r`内，存在一个余量`ρ`，使得对于满足$||w||^2+b^2≤1$ 的`w`和`b`，都有$y(<w,x>+b)≥ρ$（ρ>0），那么感知机将在$(r^2+1)/ρ^2$ 步后收敛。我们上面说只要有$y(<w,x>+b)≥0$ 就是分类正确，而 $y(<w,x>+b)≥ρ$ 说明不仅分类正确，而且还有余量。

## 感知机存在的问题
感知机不能拟合XOR函数（Minsky & Papert，1969），它只能产生线性分割面。
举个例子：现在有两个西瓜和两个苹果，两个西瓜分别在平面直角坐标系的第一和第三象限，两个苹果分别在第二和第四象限。感知机的分割只能产生一条分割线，无法正确地分类出西瓜和苹果。想要分类这里的西瓜和苹果，至少需要两条分割线。
那要怎么解决这个问题呢，那就要用到多层感知机了。

## 总结
* 感知机是一个二分类模型，是最早的AI模型之一。
* 它的求解算法等价于使用批量大小为1的梯度下降。
* 它不能拟合XOR函数，导致了第一次AI寒冬。

# 多层感知机
## 学习XOR
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051500918.png)
数据点先进入蓝色线的感知机进行学习，再进入绿色线的感知机进行学习，最后蓝色的学习结果和黄色的学习结果再进入灰色的感知机进行学习，灰色的感知机进行的时一个类似于同或的计算，然后得到最终的分类结果。
这里的 白色 相当于是输入层，蓝色和绿色相当于是隐藏层，灰色相当于是输出层。

## 单隐藏层
单隐藏层的多层感知机如下：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051507319.png)
超参数是隐藏层大小。输入层和输出层的大小一般都是根据数据和需求已经固定下来了，我们唯一可以调整改变的就是隐藏层的大小。
*超参数：开始学习过程之前设置值的参数，而不是通过训练得到的参数数据*。

### 单分类
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051515514.png)

### 激活函数
有隐藏层，就会有激活函数。且激活函数必须是非线性的。如果激活函数是线性的，那么模型通过隐藏层后的结果仍然是线性的，那其实就相当于是单层感知机了，只能产生线性分割面。而用非线性的激活函数的话，模型就有了拟合任何任何函数的可能。简单来说，激活函数的作用就是引入非线性运算。
*就像网友们分享的——“如果没有激活函数，无论嵌套多少层，输出始终可以表示为输入的线性组合。这使得拟合一些非线性函数是不可能的。”*
#### Sigmiod激活函数
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051531783.png)
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051531647.png)

#### tanh激活函数
将输入投影到（-1，1）
$$tanh(x)=\frac{1-exp(-2x)}{1+exp(-2x)}$$
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051536878.png)

#### ReLU激活函数
ReLU：rectified linear unit
$$ReLU(x)=max(x,0)$$
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051539770.png)
这个激活函数比较常用，因为计算起来比较块，不需要进行指数运算。但是仍然有缺陷，因为负半轴函数值都为零，所以在逆向参数调整时可能产生梯度消失问题。

#### Leaky ReLU激活函数
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410082219660.png)
Leaky ReLU 和 ReLU 差不多，而且，它不存在梯度消失问题。

#### 效果
效果：ReLU（其实还有Leaky ReLU） > tanh > sigmoid （与他们的导数取值范围有关）

#### 输出层激活函数如何选择
以业务需求为导向。
比如：
* 单分类问题：如果我们的目标是判断一张图片中的动物是否是猫，那么最终输出的就应该是“是猫”的单个概率值，这就可以用Sigmoid函数返回的概率来作为最终输出值。
* 多分类问题：如果我们的目标是判断一张图片中的动物是猫、狗、鼠中的哪一种，那么最终就需要三个输出值，分别为三者的概率，这时就可以用softmax函数返回每个类别各自的概率，且三者概率之和为1。
* 多标签问题：一个样本可以同时属于多个类别。比如，一张图片中同时存在猫和狗，我们可以计算这张图片中分别出现猫、狗、鼠的概率，并且其概率之和不要求为1。这里可以用sigmoid函数对这三个概率分别进行计算。计算出来结果猫和狗的概率都远大于鼠的。
* 线性回归问题：当我们面临的问题是要计算绝对的数值时（比如身高、体重、收益额等），那么最后就可以直接使用线性函数来作为激活函数。

### 多类分类
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051545676.png)
有 o1、o2、o3、ok 多种分类输出。softmax()回归就是，将这几个输出拉进一个[0,1]的区间里，将其转化为类似概率的形式进行输出，y1+y2+...+yk=1。
其流程如下：
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051552150.png)

## 多隐藏层
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410051605213.png)
当数据比较多比较复杂的时候，我们有两种策略，一种是使用很大的单隐藏层，另一种是使用第一层较大、后面逐层递减的多隐藏层。一般推荐使用第二种，这样慢慢压缩，效果会比较好。这第二种的使用中，隐藏层第一层大小一般要大于输入层，后面的层也不推荐变小后又变大，因为变小后有些数据在压缩中已经丢失了，这时再变大可能产生无用数据。但先小后大也有一些特殊情况特殊作用，比如在一些模型中可以用来防止过拟合的问题。
*所以，有些时候，这些模型的设计也难有技可寻，有时候靠的是手感去进行不断地调整（doge）。*

## 总结
* 多层感知机使用隐藏层和激活函数来得到非线性模型
* 常用的激活函数是Sigmoid、tanh、ReLU
* 使用Softmax来处理多类分类
* 超参数为隐藏层数和各个隐藏层大小

# 代码实现
[machine-learning/代码实现/MLP.ipynb at master · HeXioahei/machine-learning (github.com)](https://github.com/HeXioahei/machine-learning/blob/master/%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0/MLP.ipynb)

# 用excel模拟神经网络学习过程（阿mazing）
[【数之道 07】只需5分钟，Excel中构建神经网络模型_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1NK4y1T71u/?spm_id_from=333.788&vd_source=327f3e87e497fe83b3515199232efd15)
