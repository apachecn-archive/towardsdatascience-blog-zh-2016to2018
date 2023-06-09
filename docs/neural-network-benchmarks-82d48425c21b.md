# 神经网络基准

> 原文：<https://towardsdatascience.com/neural-network-benchmarks-82d48425c21b?source=collection_archive---------9----------------------->

我们正在经历神经网络架构的寒武纪大爆发。每个新设计都有一个基准——“它对猫的识别能力如何？”它能玩雅达利游戏吗？它能探测到停车标志吗？研究人员*使用可用的基准数据集，将他们的神经网络的性能与其他架构*进行比较。然而，这些数据集是有限的。

特别是有标签的数据，很难得到。测试非常深的神经网络需要大量的数据，并且很少有数据集大到足以允许对深度网络进行比较。因此，我们应该在*产生的*数据上测试新的神经网络。

通过生成数据，而不是管理，我们自动地给它们贴上标签。而且，生成的数据可以存在于准确性的*连续统上*，这允许我们看到一个网络是否擅长于**识别微小的错误**。这为我们提供了架构的*敏感性*和*复杂性*的度量，这在精选的数据集中是不可用的。有了生成的数据，我们可以更清楚地了解网络的学习情况，以及它在哪里出错。

**生成训练和验证数据**

作为生成数据的一个例子，考虑轨道力学:我们可以创建一个简单的软件，**在 2D 平面上随机放置“行星”**，每个都有质量、位置和速度。每次调用该软件时，它会在平面上放置一组“行星”,并在固定的时间内运行它们的轨道模型。这些样本可用于训练*和*验证，**而无需耗尽数据集**！该网络能够从任意大小的数据集进行采样——如果你想要更多的数据，只需再次调用物理软件。在训练期间，你可以很容易地生成*十亿*个样本轨道！

当软件模拟一个没有干扰的轨道*时，我们可以自动将该轨道标记为“正确的”。为了生成“不正确”的轨道，我们引入了一些*扰动*——在模拟的某个时刻，我们随机推动了一些“行星”，使它们不符合物理规律。**神经网络的任务是区分“正确的”轨道力学和“不正确的”轨道**。这是允许我们比较不同神经架构的性能的基准。*

因为我们正在**生成**我们的数据，我们可以调整*发生多大的扰动*。如果一个单独的“行星”被轻微推动，我们将其归类为“轻微不正确”。同时，当*许多*“行星”被大量推动时，我们可以将它们的轨道归类为“非常不正确”。以这种方式，**我们形成了一个*连续体*:“完全正确”→“极度错误”**。这是一个*至关重要的*能力，是猫照和手写数字所缺乏的。

**比较网络的敏感性和复杂性**

假设你想对一个新的神经网络进行基准测试，使用轨道力学软件，你给每个网络输入数十亿个轨道，并测量它们各自的精度。经过同样的训练后，两个网络都能识别出轨道何时“严重错误”——它们都能发现大的扰动。然而，你的新网络更善于识别“稍微不正确”的轨道！这表明你的新网络具有更高的灵敏度。

而且，你可以在增加“行星”数量的轨道上训练这两个网络。当只有 3 或 4 个“行星”时，两个网络都表现良好。然而，当“行星”的数量增长到 7 或 8 时，你的新网络仍然准确，而另一个网络开始失效。这表明你的新网络处理更大的复杂性。

这允许我们明确地测量**网络深度**的*值*。如果一个 4 层卷积神经网络很好地处理 3 个“行星”，但是当给定 4 个“行星”时变得有故障，那么该 4 层网络具有“3 行星复杂性”。为了诊断 4 颗或更多“行星”的轨道，我们需要增加网络的深度。

**深度人脉的价值**

通过连续增加神经网络的深度，并测试它可以处理多少个“行星”，我们得到了作为深度函数的网络复杂性的**度量**。我们可以回答结构性的问题:“*如果我把网络的深度增加一倍，我能把行星的数量增加一倍吗？*“也许，更深层次的网络处理复杂性的速度越来越快——如果一个 4 层网络处理‘3 星球复杂性’，一个 8 层网络可能在‘7 星球复杂性’上成功。如果是这样的话，**这是疯狂建立*深层网络****的最强有力的论据。*

*然而，如果深层网络变慢(例如，8 层网络仅在“5 个星球的复杂性”下运行)，这就是让许多浅层网络串联运行的理由。这是目前一个*未解决的问题*。猫照永远也回答不了。**沿着正确性和复杂性的连续体生成数据集为我们提供了一条通往答案的道路**。*