# 卷积神经网络演练—超参数调整

> 原文：<https://towardsdatascience.com/a-walkthrough-of-convolutional-neural-network-7f474f91d7bd?source=collection_archive---------3----------------------->

在多样的深度学习架构中，卷积神经网络(简称 convnets)以其在计算机视觉上前所未有的性能脱颖而出。这是一种受动物视觉皮层启发的人工神经网络，已成功应用于视觉识别任务。

在本文中，我将提供一个关于 convnet 的演练，如何调优超参数以及如何可视化隐藏的卷积层。

# 动机

首先，我们希望我们的计算机做什么？当我们看到一只猫在后院奔跑或睡在沙发上时，我们的大脑会下意识地认出它是一只猫。我们希望我们的计算机为我们做类似的事情，即把一幅图像作为输入，找出它的独特特征，并把图像标记为输出。这基本上是 convnet 能为我们做的。

# 什么是 convnet？

最基本的是，convnet 是一种特殊的神经网络，至少包含一个卷积层。典型的 convnet 结构获取图像，使其通过一系列卷积层、非线性激活层、汇集(下采样)和全连接层，以输出分类标签。

convnet 与常规神经网络的不同之处在于使用了卷积层。在常规的神经网络中，我们使用整个图像来训练网络。它对于简单的居中图像(例如居中的手写数字图像)工作良好，但是不能识别具有更复杂变化的图像(例如后院奔跑的猫)。有更多的隐藏层来学习抽象特征会有所帮助，但这相当不切实际，因为我们需要太多的神经元来训练和存储在内存中。

另一方面，convnet 通过首先寻找边缘、直线和曲线等低级特征来识别对象，然后通过一系列卷积层来建立更抽象的特征(例如什么使猫成为猫)。在卷积层的学习过程中，网络通过共享过滤器(或特征检测器)在图像的小区域上学习对象的各个部分，并将它们相加以构建抽象特征。共享滤波器的使用大大减少了实际的参数学习。convnet 还可以更好地概括复杂的图像识别，因为学习过的滤波器可以通过卷积层重新用于检测抽象特征。

# 超参数调谐

调整深度神经网络的超参数是困难的，因为训练深度神经网络很慢，并且有许多参数要配置。在这一部分中，我们简要地考察了 convnet 的超参数。

## 学习率

学习率控制优化算法中权重的更新量。我们可以使用固定学习率、逐渐递减学习率、基于动量的方法或自适应学习率，这取决于我们选择的优化器，如 SGD、Adam、Adagrad、AdaDelta 或 RMSProp。

## 时代数

时期数是整个训练集通过神经网络的次数。我们应该增加历元的数量，直到我们看到测试误差和训练误差之间的微小差距。

## 批量

在 convnet 的学习过程中，小批量通常是更可取的。16 到 128 的范围是测试的好选择。我们应该注意到，convnet 对批量大小很敏感。

## 激活功能

激活函数将非线性引入模型。通常情况下，整流器与 convnet 配合使用效果很好。其他的选择是 sigmoid，tanh 和其他激活函数，取决于任务。

## 隐藏层和单元的数量

通常最好增加更多的层，直到测试误差不再改善。代价是训练网络的计算代价很高。拥有少量的单元可能会导致拟合不足，而拥有更多的单元通过适当的正则化通常是无害的。

## 重量初始化

我们应该用小随机数初始化权重，以防止死神经元，但也不能太小，以避免零梯度。均匀分布通常效果很好。

## 转正辍学

为了避免深度神经网络中的过拟合，丢弃是一种优选的正则化技术。该方法简单地根据期望的概率删除神经网络中的单元。默认值 0.5 是一个很好的测试选择。

## 网格搜索或随机搜索

手动调整 hyperparameter 既痛苦又不切实际。有两种通用的方法来对搜索候选项进行采样。网格搜索彻底搜索给定值的所有参数组合。随机搜索从具有指定分布的参数空间中抽取给定数量的候选项。

为了更有效地实现网格搜索，最好在初始阶段从超参数值的粗略范围开始。对于较小数量的历元或较小的训练集，执行粗网格搜索也是有帮助的。下一阶段将对更多的时期或整个训练集执行窄搜索。

虽然网格搜索在许多机器学习算法中是有用的，但它在调整深度神经网络的超参数时效率不高。随着参数数量的增加，计算呈指数增长。已经发现，在深度神经网络的超参数调整中，随机搜索比网格搜索更有效(参见[关于“超参数优化的随机搜索”的论文](http://www.jmlr.org/papers/volume13/bergstra12a/bergstra12a.pdf))。根据以前的经验，结合一些对超参数的手动调整也是有帮助的。

# 形象化

如果我们可以可视化卷积层，我们就可以更好地理解 convnet 如何学习功能。两种直接的方法是可视化激活和权重。随着训练的进行，激活通常看起来更加稀疏和局部化。如果对于许多不同的输入，激活具有暗像素，则由于高学习率，它可能指示失效的过滤器(零激活图)。

训练有素的网络通常有漂亮平滑的滤波器，没有任何噪声模式。在权重中观察到的噪声模式可能表明网络训练的时间不够长，或者正则化强度低，这可能导致过度拟合。

## 参考资料:

*   伊恩·古德菲勒、约舒阿·本吉奥和亚伦·库维尔的深度学习
*   [yo shua beng io 深度架构基于梯度训练的实用建议](https://arxiv.org/abs/1206.5533)
*   [随机搜索超参数优化](http://www.jmlr.org/papers/volume13/bergstra12a/bergstra12a.pdf)
*   [卷积神经网络:架构、卷积/池层](http://cs231n.github.io/convolutional-networks/)
*   [理解和可视化卷积神经网络](http://cs231n.github.io/understanding-cnn/)
*   [通过深度可视化理解神经网络](http://yosinski.com/deepvis)
*   [理解卷积](http://colah.github.io/posts/2014-07-Understanding-Convolutions/)
*   [如何用 Keras 在 Python 中网格搜索深度学习模型的超参数](http://machinelearningmastery.com/grid-search-hyperparameters-deep-learning-models-python-keras/)