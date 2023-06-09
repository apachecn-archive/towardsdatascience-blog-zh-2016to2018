# 大女孩如何构建机器学习产品(下)

> 原文：<https://towardsdatascience.com/how-the-big-girls-build-machine-learning-products-part-ii-4ccb8ad6b6a4?source=collection_archive---------11----------------------->

你的公司或者你的团队是否在考虑利用机器学习来构建令人敬畏的产品？在第二部分*中，为了快速阅读，我在活动最后的小组讨论中总结了构建 ML 产品的最佳实践和技巧。

如果你不同意某些东西或者你想分享你的经验，请对这篇文章发表评论 o(>ω

*If you’re looking for part one, here’s the link: [大女孩如何构建机器学习产品:由产品中的女性驱动的演讲(第一部分)](https://medium.com/towards-data-science/how-the-big-girls-build-machine-learning-products-a-talk-powered-by-women-in-product-part-i-26c9a2f3e458)

![](img/e54695780638b24dcbd6696d339f9a96.png)

# 你在应用 ML 时有什么问题、恐惧或挑战？

1.  一位小组成员发现管理 ML 团队很有挑战性(如果您有类似的经历，请评论？).
2.  数据管理和处理:如何更新你的模型，加班加点，建立一个管道移动得更快？(通常，数据管理和预处理需要数据科学家大约 80%的时间)。
3.  应用程序方面，由于 ML 的存在，构建的应用程序为用户带来了真正的价值。
4.  缺乏部署和维护 ML 模型和产品的基础设施。

# 所有这些炒作是怎么回事？如何将一个问题归类为适合机器学习？

简而言之，ML 并不是万能的银弹(*闪亮的技术现象*)，有以下专家组提到的考虑因素。

## 首先从**的关键问题**开始:

*   你有数据吗？你获得它有多容易？它的容量、速度、多样性和准确性如何？如果没有数据，就不能用 ML。
*   **能否成为你产品的竞争优势？**有市场需求吗？你是在用 AI 和 ML 解决一个用其他方法解决不了的问题吗？只有当它能提供很多时，才应该使用它。确保你处理的是正确的问题，要有背景。专注于你想要完成的事情
*   如果有，**你买得起吗？**由于服务器、GPU、维护、数据科学家、经验等原因，建立一个模型非常昂贵。
*   **您的产品出错有多好？**你对假阳性和假阴性的接受程度或容忍度如何？考虑到 ML 模型不太稳定。因此，组织和清理数据是至关重要的任务。

如果以上都是肯定的，那么转到如何充分利用 ML 的技巧:你将需要反馈机制，这样你就可以随时纠正数据。有效地组织和清理数据将是关键，但在你的系统中整合反馈回路也同样重要。让你的模型不断发展变化是至关重要的。

# 分享构建 ML 产品的故事和经验

抱歉，只写了一个有趣的故事。一位小组成员分享了她的一个朋友制作的产品。这是一个会检查他的宝宝是否醒着的模型(宝宝醒着｡･ﾟﾟ*(>д

# Importance of users’ trust

When building ML products, it’s important to think of what’s the users’ perspective of the technology. You don’t want to create magic or creepy technology.

*   **了解你的用户**:小边缘情况，被冒犯的用户可能永远不会回来。您的系统必须准备好检测这种情况，并从中吸取教训。一个很好的例子是亚马逊，通过简单地改变措辞来解决这一风险:在他们建议的商品中使用“*人们也购买…* ”，而不是“*我们也推荐…* ”。降低用户对推荐系统失去信任的风险，因为当推荐系统出错时，用户会将其归咎于其他用户。
*   重新考虑你的设计:考虑那些可以把黑盒变成用户可以理解的有形概念的设计原则
*   创建界面，让人们觉得获得自己的定制体验是他们的责任。他们必须知道，他们需要参与进来，以获得定制的体验，他们对自己的体验负责。例如:“如果我有几周时间(Spotify weekly)，而他们不在我的区域内……”该客户可能会失去对该功能的信任。

# 开发流程提示

*   **获得管理层和高管的支持**:当你正在构建的产品使用了 ML，并且它对它所创造的价值至关重要时，确保你获得了高管(层级组织)或领导的支持。这些项目是昂贵的，但是当上述问题得到回答时，在非 ML 专家之间传播理解是同样重要的。
*   **数据策略&团队**:经理或策略师可能会提供很好的输入来建立数据策略。
*   **下面是 Clarifai 的 DS '部门的样子**:数据策略团队处理处理，清理数据，抓取，清理数据；应用机器学习团队，全是数据科学家；和 ML 工程师一起工作，在技术栈中进行研究、扩展和计算新的算法。重要的是，applied ML 团队不仅提供训练模型所需的数据，还开发产品并将其交付给客户。该模型集成了来自客户的反馈系统。

# 未来:景观是如何变化的？你想怎么换？

*   罗尼:将会有更多的资金，更多现成的技术和强大的计算能力。在法律方面，政策和洗钱之间的动态关系，我们需要在监管和不降低进步能力之间找到良好的平衡。
*   **埃尔希**:我们将从这个过程中学习，ML 可能会失败很多次，但我们将在管理层中传播数据责任。
*   **艾米** : " *机器人*？"。进入的障碍变得越来越无摩擦，创建和构建、部署您的模型的摩擦越来越少。一切都将有一个 ML 组件。我们将了解如何解释数据，并为更多用户创造更多价值。

# 通过多样性减少偏见

讨论以一个关于偏见的关键观点结束，这是实习者的一个普遍问题/错误，几乎无法避免。然而，我们可以通过多样性来减少偏见:性别、种族、年龄等。偏见越少，你的产品越好。提到的有偏见模式的例子是“*母乳喂养被贴上工作不安全的标签*”。就像“潜意识偏见”存在于人的大脑中一样，当它发生在 ML 模型上时，具有可比性。

抱歉发了这么长的帖子。感谢你阅读❤