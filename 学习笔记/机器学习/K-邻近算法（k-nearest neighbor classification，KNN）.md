*代码实现：[machine-learning/代码实现/knn.ipynb at master · HeXioahei/machine-learning (github.com)](https://github.com/HeXioahei/machine-learning/blob/master/%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0/knn.ipynb)*

正所谓“近朱者赤近墨者黑”，和什么样的人相处，就会变成什么样的人。数据也是一样，和某一类型的数据离得越近，就越有可能是该类型的数据。

所以，在预测数据类型的问题上，就有一种叫KNN的算法，通过与近邻数据的比对，来预测其自身的类型。

判断的依据其实有两种，一种是，你离我越近，那我就越像你，另一种是

通用步骤：
计算距离-->升序排列-->取前K个-->加权平均

K的选取：不能太大，会导致分类模糊；不能太小，会受个例的影响，波动较大

如何选取K：根据经验或均方根误差

