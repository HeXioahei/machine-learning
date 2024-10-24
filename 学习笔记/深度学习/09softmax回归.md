softmax其实用来分类的。

# 回归与分类的区别
* 回归：
	* 但连续数值输出
	* 自然区间R
	* 跟真实值的区别作为损失
* 分类：
	* 通常由多个输出
	* 输出 i 是预测为第 i 类的置信度

# 从回归到分类
## 均方损失
先对类别进行一位有效编码

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410082056733.png)

再用均方损失来训练，最后以最大值最为预测

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410082100194.png)

就是说，模型的目标是找一个和 y 一样的 i ，让 i 的置信度最大。oi 就是置信度，即预测类别是当前类别的概率，预测值 y 对于多个类别均有置信度，即有多个oi，选取oi最大的类别即为预测值。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410082106105.png)

oy是对正确类的置信度，它远大于对其他类别的置信度oi。也就是说，置信度远超其他类别的类别，即为正确类别。
## 检验比例
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410082123479.png)

# softmax函数的做法
将未规范化的预测变换为非负数并且总和为1，同时让模型保持可导的性质。
* 为使其为非负数：对每个预测求指数幂
* 为使其总和为1：每个求指数幂的结果除以它们的总和

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410222029052.png)

虽然softmax是一个非线性函数，但是softmax回归仍然是一个线性模型。
# softmax和交叉熵损失（cross-entropy loss）
![屏幕截图 2024-10-08 212327.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410082126003.png)



# softmax模型的损失函数
