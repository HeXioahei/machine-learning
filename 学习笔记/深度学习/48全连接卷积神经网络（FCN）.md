FCN是用深度神经网络来做语义分割的奠基性工具。所以他其实挺简单的。
它用转置卷积层来替换CNN最后的全连接层，从而可以实现每个像素的预测。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410091730376.png)

# 什么是转置卷积？

优质文章：[一文搞懂反卷积，转置卷积_反卷积和转置卷积-CSDN博客](https://blog.csdn.net/LoseInVain/article/details/81098502)

正常的卷积是“多对一”的一种映射关系，而转置卷积是“一对多”的一种映射关系。
正常卷积的计算公式为：（原宽 + 填充×2 - 卷积面宽 + 1）/ 步长。