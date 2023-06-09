# 一个简单的神经网络

> 原文：<https://towardsdatascience.com/a-simple-neural-network-7067e10f1c0?source=collection_archive---------5----------------------->

虽然我最近完成了 Udacity 的深度学习纳米学位项目，但我对这个学科还相当陌生。为了进一步深造，我目前正在读一本关于这个主题的优秀书籍，安德鲁·特拉斯克的 [*探索深度学习*](https://www.manning.com/books/grokking-deep-learning) *。*这篇博文的灵感直接来源于这本神奇的书。

那么，什么是神经网络？

> 神经网络是极其强大的**参数**模型，它使用矩阵和可微分函数的组合将输入数据转换为输出数据。—安德鲁·特拉斯克

换句话说，神经网络是对输入数据进行建模的一种方式，以便对该数据执行的数学函数产生有意义的结果。让我们深入研究并构建一个来了解更多信息。

```
def neural_network(input, weight):
    prediction = input * weight
    return prediction
```

这是最简单的神经网络。我们接受一个输入(真实世界的数据)和一个权重乘以输入，然后返回结果。例如，让我们说丹麦足球队在最后一场比赛中进了 3 个球。给定 0.2 的权重，我们可以用我们的神经网络预测丹麦有 60%的机会赢得他们的下一场比赛。

```
$ neural_network(3, 0.2)
$ => 0.6
```

但是我们如何找到我们的体重呢？

通过有监督的深度学习，我们可以用输入数据和实际结果来训练我们的模型，以确定权重。例如，如果我们有以下丹麦足球队的历史数据。

```
GOALS  |  WIN/LOSS
3      |  1
1      |  0
4      |  1
```

然后，我们可以告诉我们的网络从随机权重开始，计算获胜的可能性。将计算的预测值与实际的赢/输数进行比较，我们可以一遍又一遍地修改我们的权重，直到我们得到一个数字，当乘以我们的输入值(得分)时，得到一个最接近实际赢/输结果的数字。

所以，如果随机数一开始是 0.5，我们的预测将是

```
3 * 0.5 = 1.5
1 * 0.5 = 0.5
4 * 0.5 = 2
```

以此为起点，我们的网络对第一场比赛超估 50%，第二场超估 50%，最后一场超估 100%。现在有了这些信息，我们可以回过头来修改我们的权重，以减少我们预测结果的错误率。这就是线性回归的本质，本文不详细讨论。但这应该让你知道我们如何通过监督学习来确定权重，通过减少我们每次修改权重的错误率，并将我们的预测与我们的结果进行比较。

# 多端输入

在我让你为上述代码如何可能被用于驾驶自动驾驶汽车、翻译语言或赢得围棋比赛而挠头之前，让我们深入了解一个多输入神经网络。

如果我们有更多的数据来预测丹麦足球队是否会赢得下一场比赛，而不仅仅是进球数，会怎么样？假设我们知道目标的数量，他们当前的赢/输比率，以及他们拥有的粉丝数量。

```
Goals Scored  |  Win/Loss Ratio  |  No. Fans
3             |  0.6             |  30,000
```

有了更多的数据，我们可以组合多个输入来计算预测的加权和。

```
def neural_network(inputs, weights):
    output = 0
    for i in range(len(inputs)):
      output += (inputs[i] * weights[i])
    return output
```

用下面的权重取我们的 3 点输入数据，我们可以确定丹麦有 78%的可能赢得他们的下一场比赛。

```
weights = [0.2, 0.3, 0]
inputs  = [  3, 0.6, 30000]$ neural_network(inputs, weights)
$ => 0.78
```

注意，我们对应的粉丝数量权重为零。你可以想象，给定一组历史游戏数据，球迷的数量可能被证明对实际游戏没有什么影响，因此计算出的权重将接近于零。

# 积木

恭喜你！你刚刚学习了深度学习神经网络的基本构建模块之一。我们接收数据并对数据执行数学函数(在我们的例子中是乘法)来确定输出。有了更大的数据集，我们可以训练我们的网络来计算更准确的权重。在确定输出之前，我们还可以使用隐藏层来执行更多的功能。

想了解更多信息，我强烈推荐安德鲁·特拉斯克的 [*摸索深度学习*](https://www.manning.com/books/grokking-deep-learning) 和观看[西拉杰·拉瓦尔的 YouTube](https://www.youtube.com/channel/UCWN3xxRkmTPmbKwht9FuE5A) 频道。