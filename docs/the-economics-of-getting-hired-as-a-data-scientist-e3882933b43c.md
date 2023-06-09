# 要想被聘为数据科学家，不要人云亦云

> 原文：<https://towardsdatascience.com/the-economics-of-getting-hired-as-a-data-scientist-e3882933b43c?source=collection_archive---------0----------------------->

*向下滚动查看这篇文章的音频版本*

![](img/c292362e70f6aa01d74c3ec2a476da7a.png)

我还记得我哥哥决定卖掉他的比特币的那一刻。那是 2017 年，我们在星巴克。一位中年妇女向我们走来，她正在向任何愿意接受的人分发小册子。顶部用粗体字写着“比特币:提前退休之路”。

我很好奇，所以我问她对加密货币市场的看法，但事实证明，除了比特币，她不知道其他加密货币。以太坊？“没听说过。”莱特币？“那是廉价版的比特币吧？”

现在，作为一个经验法则，当甚至当地星巴克的无知的中年女士向你推销最新的科技趋势时，你可能接近炒作的顶峰。或者，如果你喜欢，一个“泡沫”。

当然，这不是一个新的观察。每个人都同意，当谈到投资时，如果你在做其他人都在做的事情，你不太可能看到任何回报。然而奇怪的是，当谈到投资*于自己*时，人们没有运用同样的推理。

假设你想被聘为数据科学家。如果你正在做所有标准的“我想成为一名数据科学家”的事情，那么这意味着你不应该指望得到你梦想的工作。市场目前充满了初级人才，因此，有抱负的数据科学家不太可能受到太多关注。所以如果你想避免中间结果，为什么要做中间的事情呢？

问题是，大多数人在开始他们的数据科学之旅时并不这样想。通过我在[sharpes minds](http://sharpestminds.com)的工作，我与数百名有抱负的数据科学家交谈过，其中大约 80%的人都有大致相同的经历:

1.  首先，他们学会了诀窍(Python + sklearn + Pandas +也许一些 SQL 什么的)
2.  然后，他们选择了某种千篇一律的 MOOC
3.  他们读了一些职位描述，担心自己不具备所需的条件
4.  也许参加另一个 MOOC，也许开始通过就业委员会申请工作
5.  听不到任何反馈(或者最多炸几个采访)
6.  感到沮丧，考虑读硕士，申请更多的工作
7.  到了一个决定点:我是否重复#2 到#7 直到不同的事情发生？

如果这种情况发生在你身上，很可能你也处在自我提升的泡沫中:你在做其他人都在做的事情，但期待不同的结果。你需要做的第一件事就是*停止*。

如果你想要高于平均水平的结果，你不能做平均水平的事情。但是为了避免做一般的事情，你需要知道一般的事情是什么。

这里有一些例子:如果你需要做 MOOC 来学习诀窍，那很好。但不要陷入 MOOC 螺旋:MOOC 几乎是为普通人设计的，所以你不会因为做得太多而成为一名优秀的候选人。同样，如果你的 GitHub 上有 4 或 5 台 Jupyter 笔记本，它们都有相同的 sklearn/Pandas/seaborn/Keras 堆栈，*不要再做一个*。

总的来说，规则是:如果某件事因为其他人都在做而看起来是显而易见的下一步，那么*最好不要做*。反过来，你需要找到别人没有做的事情，并尽快去做。

那些是什么东西？根据我所看到的，我想到了 5 个:

1.  **复印纸。如果你是深度学习爱好者，这一点尤其正确。人们不这样做，因为这比获取数据集并使用简单的 ANN 或 XGBoost 进行千篇一律的分类更难。在 arXiv 上找到与你的领域相关的最有趣的论文(最好是最近的)，并阅读它。了解一下。然后，可能在新的数据集上复制它。写一篇关于它的博文。**
2.  **不要在自己的舒适区里安逸。如果你开始一个新项目，最好是学习一些新的框架/库/工具。如果你正在构建你的第六个 Jupyter 笔记本，以`df = pd.read_csv(filename)`开始，以`f1 = f1_score(y_true, y_pred)`结束，是时候改变你的策略了。**
3.  **学习枯燥的东西。其他人没有这样做，因为没有人喜欢无聊的事情。但是，学习一个合适的 Git 流程，如何使用 Docker，如何使用 Flask 构建一个应用程序，以及如何在 AWS 或谷歌云上部署模型，这些都是公司迫切希望申请人拥有的技能，但大多数申请人都不太欣赏这些技能。**
4.  **做讨厌的事。** 1)提议在当地的数据科学会议上发表一篇论文。或者，至少，参加当地的数据科学会议。2)给 LinkedIn 上的人发冷冰冰的信息。尝试提前提供价值(“我刚刚注意到你网站上的一个打印错误”)。不要马上向他们要工作。让你的问题尽可能具体(“我很想在我的博客上得到你的反馈”)。你试图建立一种关系，扩大你的网络，这需要耐心。3)参加会议和网络。4)成立学习小组。
5.  做一些看起来疯狂的事情。每个人都去 UCI 知识库，或者使用一些股票数据集(哈欠)来构建他们的项目。不要那样做。了解如何使用 web 抓取库或一些不太受欢迎的 API 来构建您自己的自定义数据集。数据很难获得，公司通常需要依靠他们的工程师来获取数据。你的目标应该是给人一种痴迷于数据科学的疯子的印象，如果这是完成工作所需要的，他会建立自己的数据集。

这些策略中的每一个都是另一种摆脱招聘者每天面对的噪音的方法。它们都不是灵丹妙药，但它们是在数据科学就业市场上获得更多吸引力并成为更有能力的数据科学家的可靠方法。

在一天结束的时候，记住当你在培养自己的技能时，你是在投资自己。这意味着适用于投资的所有经济原则在这里都适用:如果你想要一个出色的结果，你必须做出色的事情。