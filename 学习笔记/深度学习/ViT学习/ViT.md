![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411070918355.png)

对于标准的transformer模块来说，要求输入的是tokens序列，而每个token是一个向量，则tokens序列即为一个二维矩阵`[num_token, token_dim]`。

我们要对一张图片进行分类识别，直接将一整张图片作为一个token显然无法提取图片中的特征信息。所以我们要对图片进行分割，分割后得到的每一张小图片作为一个输入，生成一个token。

那要如何分割呢？卷积的特性刚好可以做到这一点。比如我们有一张`[224*224*3]`的图片，那么，我们可以用`[16*16]`大小的卷积核，以`stride=16`来进行卷积，这样就可以把图片分割为