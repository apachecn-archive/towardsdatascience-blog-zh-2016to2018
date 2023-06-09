# 依靠事实——专家意见有什么价值？

> 原文：<https://towardsdatascience.com/banking-on-the-facts-54ea1704c270?source=collection_archive---------4----------------------->

![](img/6d4dbceb469bb97c80f03aa9c4b26c83.png)

Maptive

几年前，当我开始下一项任务时，我接待了三位新同事的来访。我很惊讶地听到第一个人承认“在这里你必须学会的第一件事是，每个人都在所有事情上撒谎”。第二个来访者不再令人鼓舞地证明只有她一个人说了实话。第三个来访者——正如他们在法语中所说的“没有三个人的两个人”——试图让我“放心”，如果前两个人说实话，他们会被闪电击中。在一个虚伪的世界里，人们要么永远诚实，要么永远虚伪，我的三个来访者中，哪一个值得相信？[【我】](#_edn1)

在一个越来越以假新闻和另类事实为标志的后真相世界里，这个故事在我的脑海中依然清晰可见。尽管同事们公然歪曲数据的情况非常罕见，但区分事实和虚构绝非易事。当今管理面临的复杂问题挑战了真理的单一版本的概念。这些挑战使得选择最佳行动方案变得更有价值，无论是在鉴定业务的“无形资产”、提高管理效率还是衡量客户满意度方面。征求专家的意见并不能解决很多问题，因为他们通常更愿意回忆过去，而不是规划未来。如果经理的工作是根据事实做出决定，他或她怎么能指望专家的建议呢？

*为什么如此多的专家，即使是真诚的，也只能提供可怜的建议？*风险、不确定性和模糊性等不利因素通常会阻碍专家客观评估新挑战的能力。依赖“机器学习”并不能解决问题——对于许多关键变量，每个算法都依赖于这些专家的主观估计。他们的建议意见很少因为他们对这些模型的信任而调整——他们计算客观概率，而不考虑他们自己的偏见、怀疑和对手头问题的理解。Julia Galef 将这种倾向称为“动机推理”，专家(像大多数其他人一样)倾向于优先考虑与他们自己的精神状态相对应的数据。[【ii】](#_edn2)套用幽默作家乔希·比林斯的话*“问题不在于你的专家们知道什么，而在于他们如何确定事实并非如此”。*[【iii】](#_edn3)

无需求助于昂贵且耗时的“大数据”和“人工神经网络”,可以使用几种相对简单的方法来证实并最终校准专家的观察能力。正如道格·哈伯德(Doug Hubbard)所建议的，将适当的方法应用于非常小的样本可以大大减少不确定性的来源。他提倡“五法则”，即评估一个分布的五个随机估计值提供了 93 . 5%的置信指数，即它的中值在最低和最高估计值之间。类似地，捕获/再捕获方法基于超几何分布有效地估计大种群的规模。[【VI】](#_edn6)定点取样提供了另一种选择，它随着时间的推移随机拍摄现象的快照，而不是不断地跟踪它们。最后，通过简单地识别随机的一组观察值，然后与该组一起采样，聚类采样产生了令人惊讶的好结果。[【VII】](#_edn7)

本文开头的谜语是“骑士和无赖”谜题的一个应用，我们假设骑士永远不会说谎，而无赖永远不会说真话。因为陈述是矛盾的，在测试假设时，只有第二个来访者内心是真实的。在商业中，背景和解决方案都更加复杂，因为事实和虚构之间的界限往往很模糊。学会利用手头的数据来支持或配合每个专家的观点可以帮助我们减少专家自身认知偏差的影响。提高决策能力是商业分析学院、暑期学校和大师班的核心。提高自己的决策能力只需点击一下鼠标。

Lee Schlenker 是 Pau 商学院的教授，也是 http://baieurope.com 商业分析学院的负责人。 *他的领英简介可以在【www.linkedin.com/in/leeschlenker.】[*查看*](http://www.linkedin.com/in/leeschlenker.) *你可以在*[*https://twitter.com/DSign4Analytics*](https://twitter.com/DSign4Analytics)关注我们的推特*

_________________

[【I】](#_ednref1)改编自 Smullyan，R. (1978)。这本书叫什么名字？。普伦蒂斯霍尔

[【ii】](#_ednref2)Galef，J. (2016)，人类擅长辩论，却不擅长推理。Heleo 对话

[【三世】](#_ednref3)比尔盖茨，J. (1874)。智慧和幽默的百科全书和谚语哲学

贝叶斯定理将在另一篇文章中展开。

Hubbard，D. (2014)，如何衡量任何事物:寻找商业中“无形资产”的价值

[【VI】](#_ednref6)【马】d .(2010)捕获/再捕获方法，概率统计博客

[【VII】](#_ednref7)统计技术。(2017)，[什么是整群抽样？](http://stattrek.com/survey-research/cluster-sampling.aspx)