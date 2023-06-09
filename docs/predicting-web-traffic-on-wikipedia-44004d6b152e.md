# 预测维基百科的网络流量

> 原文：<https://towardsdatascience.com/predicting-web-traffic-on-wikipedia-44004d6b152e?source=collection_archive---------4----------------------->

# 现场 Kaggle 比赛

![](img/e26c7b94f88b7c4e9ce608b1f39cf5cc.png)

这是我在 Kaggle 上参加 WTF 比赛的文档，这是网络流量预测的简称！一个月不稳定的管道建设，一些令人沮丧的周末，40 次提交和 22 次提交后，我仍然没有达到我的期望。虽然学到了很多，但这份报告是试图组织学习。

*也就是说，一个警告——这个博客会稍微有点技术性:)*

![](img/47da1c2e2d46047396aae9f9ee550b6a.png)

这是一场现场比赛，由 Kaggle 主办，由 Google 发布 145K 维基百科页面的网络流量将在 2017 年 9 月至 11 月期间进行预测，这意味着，我们提交的准确性将实时计算——取决于未来如何发展！训练数据由过去两年中维基页面上每天的查看次数组成。

听起来像一个非常标准的时间序列问题，对吗？大错特错。

**我的方法——**[**Github**](https://github.com/shubh24/web_traffic_prediction)

在我的脑海中有一个面向 xgboost 的策略并不总是很好，这个竞争让我离开了我的舒适区！很自然地，我查阅了关于 ARIMA 模型表现的讨论/内核——显然，自回归模型不能很好地推广到目标变量的未知范围(这是我们问题中非常可能出现的情况)。

一对夫妇的方法脱颖而出:

*   将时间序列问题建模为回归问题，每个页面-日期对被视为一行。
*   使用脸书的预言家，他们的新预测工具。

在一些顶级 kagglers 的建议下，我决定采用回归模型——将基于时间序列的数据框架融合到传统的每行页面日期特征数据框架中。运行 xgb，并在类似熔化的测试数据帧上进行预测。

**特征工程**

![](img/3a2052219dd04bdb731bfa7bd87e65c3.png)

*总体平均值/中值* —一个简单的常量提交，包含过去 8 周的平均值/中值，在第一阶段很难被超越。包括在内。

*滚动方式和滚动中间值*——这些是我想到的一些最明显的特性，然而它们实现起来并不简单。我同意，在预测今天的流量时，过去 7 天的滚动平均值将是一个重要的特征，但挑战是要求我们预测未来三个月的流量数据。

当当前日期是 9 月 14 日时，如何找到 11 月 1 日的周滚动平均值？

因此，像滚动平均这样的功能在验证中表现非常好，但在公共排行榜上却不是这样。最后，我继续使用过去 30 天和 60 天的滚动平均值和中间值。对于我无法计算这些特征的日期，我继续使用时间序列中最后一个可用的计算特征的代理。

后来，我包括了更多的功能，如滚动标准开发，滚动最小/最大等。

*基于工作日的平均值/中值* —这些特性被证明是最重要的特性之一！很明显，很多维基百科的点击是工作日/周末相关的——我试图通过过去六个月的工作日累计平均值和中值来捕捉这一点。

*语言和来源*——我试图整合来自页面语言或来源(爬虫、蜘蛛等)的统计数据，但这些并没有让我在一个普通的 xgboost 上得到提升。为了简单起见，把它们去掉了。

*最后一天的访问*——像**最后一天的访问**这样的特性在进行验证运行时非常有用。测试数据并非如此，因为竞争是实时的。我必须提交对未来两个月所有页面的预测——显然，使用最后一天的访问量是愚蠢的！

**流水线作业**

构建一个抽象的模块化管道占用了我大部分的带宽！我必须将宽格式的数据帧转换成长格式的数据帧，并对每个页面-日期对进行滚动统计。计算每个滚动统计的函数有可选参数，如“last _ n _ days”——30 天的滚动平均值，以及“rows _ to _ consider”——我们希望返回多少个日期。

在大量阅读内核和论坛之后，我坚持许多顶级 kagglers 的策略:

*   在所有页面上训练一个 Xgboost 模型。这将帮助我们确定整个维基百科的总体趋势。
*   在网页的所有未来日期上测试模型。

另一种方法是在每个页面上单独训练一个 xgboost，使算法个性化。这非常耗时，并且可能无法很好地推广。

**型号**

> *XGBoost 是爱，XGBoost 是命！*

![](img/17875f5bdf9d8e354e716cea1ad28f05.png)

我继续与香草 xgb，再一次。首先，xgboost 在几个月的讨论中得到了很好的反馈。这是我第一次使用自定义损失函数( [SMAPE](https://en.wikipedia.org/wiki/Symmetric_mean_absolute_percentage_error) )作为 xgboost 参数(feval)，这是一个有争议的损失函数选择——不可微且不对称！

我面临的一个主要问题是，基于树的模型不能很好地推广到未知的范围，在我添加更多功能之前，与 xgboost 的常量预测斗争了一段时间！解决这个问题的方法是将目标变量的差异视为目标变量，从而限制范围。这需要以类似的方式改变特性，我没有走这条路。

**挑战&失误**

![](img/2dd3ceed23c3d47b6e2b775d12ade08a.png)

*   XGBoost 不能很好地推广到未知范围，如前所述。
*   由于我将数据帧分解为长格式，如果我只考虑最近六个月的数据，那么行数达到了 2600 万！这是其中的一个权衡，放弃旧数据而不是 RAM 限制。
*   正如我前面提到的，在测试数据集中计算未来几天的滚动统计是不可能的。我试着把它们设为 NA，但这大大夸大了预测(因为模型在训练中没有看到 NA)。最后，我坚持向前填充滚动统计数据。
*   建了一个复杂的管道，调试简直是一场噩梦！我还是想不出更简单的方法，权衡:)
*   我的 noob 错误——将数据帧的浅层副本视为深层副本。我怎么也想不出这个 bug！

**学习成果&结论**

我从这次比赛中得到的主要收获是:

*   花更多的时间在 kaggle 讨论上，并且经常参与。这将建立一个循环——工作、讨论。讨论，工作。
*   应该从一开始就抽象我的功能。重构一点都不好玩！
*   我想我已经刷爆了我的功能，现在要看看别人提交的内容了！
*   既然我擅长流水线和特性工程，我应该更加关注模型调优和集成。
*   不要害怕时间序列问题。在一天结束时，它的好 ol '回归！

总的来说，这是一场有趣的比赛——现在想起来，可能更令人沮丧而不是有趣！学到了很多，对我将来的比赛很有帮助。

![](img/5422f1dc9a733025162391bb8f8655a7.png)

到下一个:)

*这篇文章最初发表在我的* [*博客*](https://shubh24.github.io) *上。每周一篇博客*