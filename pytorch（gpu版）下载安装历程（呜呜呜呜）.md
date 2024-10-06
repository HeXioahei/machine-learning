最开始，是在三天前，刚开始学深度学习，需要用到pytorch，就直接上网络上找下载的教程了，当时是跟随着这个教程进行下载的：[在Anaconda下安装Pytorch的超详细步骤_anaconda安装pytorch-CSDN博客](https://blog.csdn.net/qq_45281807/article/details/112442423)。同时，我也对anaconda的使用有了进一步的了解，学会了如何在anaconda用命令行创建新的环境以及如切换环境。不过需要提醒的是，这篇文章虽然写的很不错，但是有些地方没有说明清楚，建议先看评论区。（经验：看博客文章之前，一定要先看评论区）

然后就是昨天晚上，跟着视频课程实现代码，在训练模型的时候，虽然指定了用gpu来运行，但是仍然只能用cpu来运行，速度很慢，也怕电脑吃不消。

所以，今天早上就开始找原因，最开始是看到这篇文章： [PyTorch GPU利用率为0%（很低）使用pytorch训练模型为什么gpu占用为0-CSDN博客](https://blog.csdn.net/qq_45831414/article/details/135556280)，知道了如何检测GPU是否可用以及失败的可能原因有哪些（提到了很多没听过的新东西）。但是解决方案有点看不懂，就换了一篇文章。接下来就看到了这篇文章：[［超级详细］如何在深度学习训练模型过程中使用GPU加速_电脑中如何使用gpu跑模型-CSDN博客](https://blog.csdn.net/qq_52730883/article/details/130650143#:~:text=%E5%89%8D%E8%A8%80.%20%E5%9C%A8%20%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0)。这篇文章详细介绍了在深度学习训练模型前为了使用GPU加速而进行配置的步骤教程。由于电脑类型不同，所以在下载相关资源文件的时候要十分注意版本，比如显卡的型号以及当前虚拟环境下所用的python版本，版本的适配在后续是十分重要的。就在这篇文章的帮助下，我成功下载安装了CUDA和cudnn（仔细看文章的步骤，包括他中间插入的推荐链接）。

我本来以为这样就差多不可以了，但是后来训练模型时发现GPU还是没有被使用。就又开始搜索原因。中午的时候得知，原来根本原因在于，三天前下载安装pytorch时，使用清华大学的镜像源下成了cpu版本，所以只会使用cpu。于是，就开始准备重新创建一个环境，重新下载gpu版的pytorch。

首先遇到的难题就是版本的适配，我查官网、查最新文章，试图知道最新版本的cuda、cudnn都分别适配什么版本的pytorch、python、torchvision。因为我早上已经下载并配好了最新版本的cuda（v12.6）和cudnn（v8.9.7）了，不想删了重下重配，但是不巧的是，大部分文章教程里的版本都不是最新的。所以适配起来花了挺多时间。分别看了这些文章：
* [【Pytorch、torchvision、CUDA 各个版本对应关系以及安装指令】_pytorch版本和cuda版本关系-CSDN博客](https://blog.csdn.net/crist_meng/article/details/136425444)
* [PyTorch碎片：PyToch和Torchvision对应版本_pytorch与torchvision版本对应-CSDN博客](https://blog.csdn.net/jorg_zhao/article/details/106883420)
* [pytorch安装: cuda、cudatoolkit、torch版本对照 - coffeeMA - 博客园 (cnblogs.com)](https://www.cnblogs.com/jacexu016/p/18409959#:~:text=%E5%8F%AF%E4%BB%A5%E9%80%9A%E8%BF%87%20nvidi)（这篇文章是我找到的最新发布的，所以里面展示的版本适配也是最新的）
差不多知道分别需要哪些版本后，就要开始看怎么下载和安装了。查看pytorch官网[Start Locally | PyTorch](https://pytorch.org/get-started/locally/)，最新版本的pytorch是v2.4.1，适配的CUDA最新版本为v12.4，和我的v12.6不一样，找了一些文章并看了评论才知道，v2.4.1的pytorch和v12.6的CUDA也是适配的。于是就开始下载。直接从pytorch官网复制命令到anaconda prompt进行下载，但是刚开始下一点点就停止了。报错如下：![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062044677.png)
试了两次都不行，梯子也搭了。看到第二次有动一点点我还很激动呢，但是一会儿就停住了，我也不是很清楚是什么原因，感觉可能是网络问题，因为一般国外官方的东西都没那么容易下载。就开始打算使用清华镜像了。找到了这篇文章：[conda安装GPU版pytorch，结果却是cpu版本[找到问题根源，从容解决]为什么conda安装pytorch版本不对-CSDN博客](https://blog.csdn.net/u013468614/article/details/125910538#:~:text=%E6%9C%AC%E6%96%87%E8%AF%A6%E7%BB%86%E5%88%86%E6%9E%90%E4%BA%86con)，写的很好，他的点赞量和收藏量也说明了一切。这篇文章解释了为什么明明下载的是cpu版本的pytorch结果确实gpu版本，也让我知道了如何区分这两个版本等等。文章的最后提到了如何下载pytorch镜像。我依葫芦画瓢，在精华镜像网站寻找有哪些版本是适配且可下载的，但是没有成功，报错如下：![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062054390.png)
也不是很清楚是什么原因。我还试了直接在清华镜像网站把对应的资源压缩包下载，然后解压后放进anaconda的pkgs目录下，没有效果。在此之前，我还试过直接在anaconda navigator 里搜索pytorch并下载，但是显示无法获取资源，也就没有成功了。![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062058591.png)
我去找别的学校的我的同专业高中同学帮忙，他说他就直接官网命令复制然后再命令行中运行，没用梯子就下好了。我很震惊，所以，我又试了几次直接官网命令下载，终于，它不会突然断掉了，成功下载好了。后来进行模型训练，也成功用gpu跑了起来，速度也快多了。得到了结果：![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062102874.png)

以上皆只是我的探索历程，整理一下，去掉没用的步骤，我总结的完整的下载安装流程如下：

* 首先，按照这个教程下载好CUDA和cudnn：[［超级详细］如何在深度学习训练模型过程中使用GPU加速_电脑中如何使用gpu跑模型-CSDN博客](https://blog.csdn.net/qq_52730883/article/details/130650143#:~:text=%E5%89%8D%E8%A8%80.%20%E5%9C%A8%20%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0)
* 然后，根据这篇文章[pytorch安装: cuda、cudatoolkit、torch版本对照 - coffeeMA - 博客园 (cnblogs.com)](https://www.cnblogs.com/jacexu016/p/18409959#:~:text=%E5%8F%AF%E4%BB%A5%E9%80%9A%E8%BF%87%20nvidi)所说的版本的适配，创建新的python环境（如果原环境下python版本本身就适配，就不用创建新的环境了），去官网复制对应版本的pytorch下载命令，到anaconda prompt下运行（如果下一半就断掉，那就重新运行）。
* 最后检测是否配置成功：
	在python终端（注意，是终端，就是黑黑的窗口里）输入如下命令：![image.png](https://youki-1330066034.cos.ap-guangzhou.myqcloud.com/machine-learning/202410062119411.png)
	版本的结果若是cu，则说明是gpu，最终输出true，则说明可以成功调用gpu。

另外，我的显卡型号为
所以，这么一看，其实正确的步骤过程也没有很复杂。