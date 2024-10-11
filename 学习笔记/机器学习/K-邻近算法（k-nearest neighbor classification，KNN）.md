*代码实现：[machine-learning/代码实现/knn.ipynb at master · HeXioahei/machine-learning (github.com)](https://github.com/HeXioahei/machine-learning/blob/master/%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0/knn.ipynb)*

寻找最近的K个数据，推测新数据的分类。

通用步骤：
计算距离-->升序排列-->取前K个-->加权平均

K的选取：不能太大，会导致分类模糊；不能太小，会受个例的影响，波动较大

如何选取K：根据经验或均方根误差

