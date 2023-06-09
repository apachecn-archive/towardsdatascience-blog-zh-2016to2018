# 迈克·特劳特将在休赛期得到一份终身合同…但是他应该接受吗？

> 原文：<https://towardsdatascience.com/mike-trout-is-going-to-be-offered-a-lifetime-contract-this-offseason-but-should-he-take-it-190555642395?source=collection_archive---------6----------------------->

预测 MLB 未来的薪水能帮助特劳特做决定吗？

![](img/801ef00b950224226f5a26df54e53082.png)

2 time AL-MVP Mike Trout

1984 年，魔术师约翰逊为洛杉矶湖人队签下了历史上最赚钱的合同之一:25 年，2500 万美元。本质上，湖人给他提供了有史以来第一份“终身合同”，以显示他们对他的忠诚，并确保他们会锁定他的剩余职业生涯。显然，魔术师不会在他 2009 年结束的合同结束时一直打球(他在 1996 年退役)，但在 1984 年，人们不可能想到有人会签下 2500 万美元的合同。

快进到 2018 年，我们认为如果一名运动员签了一份 2500 万美元的合同，那他就弄错了。合同似乎每年都在突破极限，看不到尽头。像斯蒂芬·库里(Steph Curry)和拉塞尔·威斯布鲁克(Russel Westbrook)这样的 NBA 明星每年赚 4000 万美元，MLB 投手扎克·格雷因克(Zach Greinke)和克莱顿·克肖(Clayton Kershaw)每年赚 3000 多万美元，甚至 NFL 也开始向四分卫和外接手发放 2500 万美元的薪水。

因此，当你有一个像迈克·特劳特这样的全宇宙棒球运动员接近自由球员，在过去 150 年里以超过所有人的水平打球，那将是一笔巨大的支票。特劳特已经是 MLB 最高位置的球员，预计在 2020 年前每年可以赚 3225 万美元。似乎这还不够，棒球专家们期待他将成为体育史上第一个签署 4 亿美元总价值合同的球员。

为了留住这一代最伟大的球员，他目前的球队洛杉矶天使队决定向他提供一份终身合同，在可预见的未来锁定他。天使们可以为他提供大量不同的选择，但如果你是迈克·特劳特，你会如何谈判这笔交易？签下合同锁定未来 20 年的职业生涯有意义吗，还是应该看看自由代理能带来什么？

我决定看看历史上 MLB 的最高工资，以预测未来几年 MLB 的工资会是什么样子，以及在自由球员时代，特劳特应该如何评价自己。

对于那些对时间序列分析更感兴趣的人来说，这个项目的代码可以在 https://github.com/anchorP34/MLB-Salary-Predictions 的[](https://github.com/anchorP34/MLB-Salary-Predictions)**查看。像往常一样，留下你对这个主题的其他想法或你感兴趣的其他分析的评论。**

*职业运动员赚的钱多得离谱，但情况并不总是如此。1930 年，贝比·鲁斯是第一个收入超过美国总统的职业运动员。所以当我们回顾 MLB 每年最高工资的历史时，我们真的没有看到财富的大幅增长，直到大约 80 年代和 90 年代*

*![](img/2aa8eb28f6a48b2725c0d76eaabdccc9.png)*

*Information provided by [https://sabr.org/research/mlbs-annual-salary-leaders-1874-2012](https://sabr.org/research/mlbs-annual-salary-leaders-1874-2012)*

*由于预测 2020 年的工资不会受到 19 世纪和 20 世纪初工资的影响，我决定将分析缩减到二战后(1945 年至 2018 年)。*

*![](img/51c2993db6421b70e7c863cb7e23acb7.png)*

*对于任何类型的预测/预测问题，尝试找出任何使预测更容易计算的转换都是重要的一步。从上面的图表中我们可以看出，随着年龄的增长，工资呈指数增长趋势。因此，取指数函数(自然对数)的倒数将得到一个更线性的函数。*

*![](img/cbf101ca68c69efeb6709e43baf8ad21.png)*

*这更容易处理。有了线性线，我们可以采用指数平滑预测模型来预测转换后的数据，从而在模型中给出更准确的预测。*

*![](img/4aa98d682e4fd70d600a27f704aa8adf.png)*

*Time series analysis using different methods and forecasts*

*从表面上看，这些模型似乎非常符合这一趋势。然而，告诉某人 2020 年最高工资的自然对数将大约是 17.5 对任何人都没有帮助。因此，我们需要将数据“反转换”回其原始形式，并将模型从自然对数转换回指数形式。*

*![](img/873556c3fb4dfce00e4ebe28956a7fb7.png)*

*1990 was a good year to test a CAGR model since that is where salaries really started to explode*

*从图中可以看出，霍尔特指数模型比简单指数模型更激进一些，后者似乎认为工资会趋于平稳。我提出的另一个预测是 1990 年至 2018 年的 CAGR(复合年增长率)，这只是该时间段工资的平均复合增长率。CAGR 模型比霍尔特指数预测的斜率更陡，所以我决定使用霍尔特指数模型来预测未来的工资，因为它是其他模型之间的一个很好的分割。*

*根据 Holt 模型，当 Mike Trout 成为 2021 赛季的自由球员时，MLB 的预测最高工资将为 42，752，450.05 美元/年。*

*就特劳特谈判他的薪水而言，这意味着什么？首先，2021 年的预测工资比他现在的工资高出大约 1000 万美元。如果天使们给特劳特加薪，我会建议至少给*提供预计的 2021 年的*。这一年他将能够在自由球员中检验他的价值，所以他们也可以提前几年。每个职业中的每个人都想得到自己的价值，所以从天使的角度来看，在他成为自由球员时支付最高工资将证明适当的忠诚水平。*

*![](img/825ca37502e448658cdb99ff6d809d68.png)*

*然而，从特劳特的角度来看，如果他现在就拿这笔钱，而不是等到自由球员时代，会有什么不同吗？很难说在好莱坞生活同时拿着 8 位数的薪水是不可能被击败的，但是特劳特来自东北部，为什么像费城费城人队这样的球队不会为像他这样的球员支付那么多呢？等到自由球员时代或者现在签约，在经济上有很大的不同吗？*

*计算方法是，从休赛期开始，到 2031 赛季，也就是他 40 岁结束这一年，现值年金为 42，752，450.05 美元。我使用了 3%的贴现率来补偿通货膨胀，因为今天的 100 美元在十年后会超过 100 美元。这就是左侧图表中的终身交易 PV。*

*没有终身的 PV 涉及到迈克特劳特坚持己见，等待他的合同到期，直到他成为自由球员。那就是取他现在合同的现值，然后取 2021 年到 2031 年的 42，752，450.05 美元的贴现年金。*

# *迈克，现在不要拿钱！*

*除了因为接受终身合约而没有获得 1000 万美元的加薪而损失一些钱之外，特劳特还将在 13 年内损失 1600 万美元的机会成本。与不签终身合同的 4.38 亿美元现值相比，这仅仅是他终身总工资的 4%左右的增长。在最初几年，是的，1.04 亿美元与 1.2 亿美元相比是一个很大的差异，但 4.38 亿美元到 4.54 亿美元*你可以选择你和你的家人将在哪里度过你的余生？**

*这甚至不是一个讨论迈克，等着看你能在自由市场赚多少钱。*