![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411070918355.png)

对于标准的transformer模块来说，要求输入的是tokens序列，而每个token是一个向量，则tokens序列即为一个二维矩阵`[num_token, token_dim]`。

我们要对一张图片进行分类识别，直接将一整张图片作为一个token显然无法提取图片中的特征信息。所以我们要对图片进行分割，分割后得到的每一张小图片作为一个输入，生成一个token。

那要如何分割呢？卷积的特性刚好可以做到这一点。比如我们有一张`[224,224,3]`的图片，并且要求`ptaches=16`（即切割成一张张`16*16`的小图片），那么，我们可以用`[16,16]`大小的卷积核，以`stride=16`来进行卷积，这样就可以把图片分割并缩小为一张`[14,14,1]`的特征图（每个像素点都是由`16*16`的小图片提取出来的）。假设卷积核有768个，则输出即为`[14,14,768]`。

再进行扁平化处理（Flatten）拉长为一个向量`[1,196,768]`，768是卷积中的通道数个数。196即为还没加上class token时的token数。

至此，patch embedding就完成了。

经过patch embedding层之后，就变成了`[196,768]`的二维矩阵，也即tokens序列。再加上class token，就变成了`[197,768]`。

再通过position embedding层，叠加position参数（可学习的参数），（直接进行相加操作），仍然是`[197,768]`。

用余弦相似度来求位置相关性，得到位置编码。（这里还是没看懂）

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411070954790.png)

transformer encoder 层就是将encoder block 堆叠 L 层得到的。在encoder block中，先是通过了layer norm 层，进行标准化处理。然后通过muti-head层后，再通过dropout层进行正则化处理，再进行一个类似于ResNet的残差相加操作，再以类似的步骤通过MLP层。

其实，在transformer encoder前还有个dropout层，后有一个layer norm层。

而MLP Head层是由一个Linear层构成的，如果数据集很大的话，也可能是Linear+tanh+Linear三个部分。

![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202411071513361.png)

还有一种混合模型HyBrid（cnn+transformer）。在数据较小的时候，混合模型的精度会更高一些，在数据大的时候，ViT的效果会比HyBrid好。

博主gihub：WZMIAOMIAO.