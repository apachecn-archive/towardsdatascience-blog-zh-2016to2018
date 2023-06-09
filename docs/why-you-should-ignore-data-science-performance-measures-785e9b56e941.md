# 为什么您应该忽略数据科学绩效评估

> 原文：<https://towardsdatascience.com/why-you-should-ignore-data-science-performance-measures-785e9b56e941?source=collection_archive---------4----------------------->

![](img/c2b991629c9f3ec42b55df7a637d41d7.png)

Picture by [Peter Belch](https://stocksnap.io/photo/9PYY07X93T), CC0

上周，我拜访了一位客户，向他展示了我的分析。我显示的 AUC 是 0.92。印象深刻，嗯？

你不知道我在说什么？太好了——你不需要。有一堆数据科学性能指标。AUC、AUPRC、F-Measure、R-Squared、RMSE、精确度等等等等。在现实生活中他们都不会帮到你。你应该简单地忽略它们。

# 优化你真正想要的

如果做行业内的数据科学项目，你对什么感兴趣？收入？延迟时间？那么你为什么不对此进行优化呢？每个数据科学项目都应该针对其目标价值进行优化。在最好的情况下，数据科学绩效评估只能代表您的真实目标。分类比较正确当然好。当然，确保预测和目标变量之间的良好相关性是很好的。但这只是一个代理，而不是主要目标。

# 为什么它会对您优化的内容产生巨大影响

先说一个简单的例子。您的目标是减少银行账户的流失，包括个人账户和企业账户。你可以想象有几种类型的客户流失者。

可能会有学生、工人，也可能会有初创企业和更大的公司流失。简单地以最准确为目标是好的，但是我们通过为学生预测它来产生多少收入呢？没那么多。中型公司呢？我想会更多。\ n * *因此，我们的绩效指标以及优化方案应该考虑每个客户的收入，并更多地关注大客户。**找到更少的产生更多平均收入的搅动者可能比简单地找到尽可能多的人更好。