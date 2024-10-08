softmax其实用来分类的。

# 回归与分类的区别
* 回归：
	* 但连续数值输出
	* 自然区间R
	* 跟真实值的区别作为损失
* 分类：
	* 通常由多个输出
	* 输出 i 是预测为第 i 类的置信度

# 从回归到分类——均方损失
先对类别进行一位有效编码
![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410082056733.png)
再用均方损失来训练