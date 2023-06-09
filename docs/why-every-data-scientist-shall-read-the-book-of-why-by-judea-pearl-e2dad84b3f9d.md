# 为什么每个数据科学家都应该阅读朱迪亚·珀尔的《为什么之书》

> 原文：<https://towardsdatascience.com/why-every-data-scientist-shall-read-the-book-of-why-by-judea-pearl-e2dad84b3f9d?source=collection_archive---------6----------------------->

## 因果关系如何进一步推进数据科学和人工智能

我做了 4 年机器学习和一年多深度学习的忠实粉丝。我为娱乐和工作建立了预测模型。我知道很多算法，从像梯度推进这样的传统算法到像 LSTM 这样的最深模型。尽管我已经获得了无数的算法，我的困惑依然存在。

![](img/9e2be94f55013429448bf958f15cde59.png)

**算法本身无法解决的难题**

如果你不是那种只关心如何减少 0.01%的误差，但试图理解你的模型的数据科学家，你可能会不时地问自己:

1.  我应该把这个变量添加到我的模型中吗？
2.  为什么这个反直觉的变量显示为一个预测变量？
3.  为什么我再加一个变量，这个变量会突然变得无关紧要？
4.  为什么相关性的方向和你想的相反？
5.  为什么在我以为会更高的时候相关性为零？
6.  当我将数据分解成子群体时，为什么关系的方向会反转？

随着时间的推移，我已经建立了足够的意识来解决这些基本问题，例如，我知道双变量关系可能与多变量关系非常不同，或者数据会受到选择偏差的影响。但它缺乏一个坚实的框架，我可以肯定地说服自己和其他人。更重要的是，我可能不会意识到，直到一段关系与我的感觉相矛盾！重要的是要注意，当有矛盾时，它已经出了大问题。没有地图，在我知道自己迷路之前，我怎么能确定我没有走错目的地呢？

**是的，联想和因果都可以预测**

当我读到朱迪亚·珀尔的《为什么之书》时，这个困惑已经完全消失了。现在它是我的数据科学指南。这里我简单告诉你为什么。简而言之，就是因果关系，因果关系。预测未来有两种方法:

1.  我知道看到 X，就会看到 Y(联想)
2.  我知道 X 导致 Y(因果关系)

两种方式都可以预测。这两种方法可能会产生相似的模型性能。那么，有什么区别呢？为什么要费心去理解因果关系？如果它是一个更强大的工具，因果关系可以通过数据来研究吗？

**随机对照试验以及为什么有时不可行**

作为金标准，随机对照试验(RCT)(或市场营销中所谓的 A/B 测试)用于测试因果关系。特别地，在临床试验中，该技术用于研究特定药物/治疗是否可以改善健康。

随机化是为了**最小化选择偏差**，以便我们知道，例如，我们不会选择性地将治疗应用于更多的患病患者，从而导致明显更低的收益，如果我们不选择更多的患病患者，就不会有这样的收益。对照是作为一个基准，以便我们可以比较接受治疗患者和未接受治疗的患者。作为一种标准，还有一种所谓的双盲机制，使患者不知道他们是否实际接受治疗，以屏蔽心理影响。

虽然这是黄金标准，但在某些情况下可能不可行。例如，如果我们想研究吸烟对肺癌的影响，显然我们不能强迫某人吸烟。另一个例子:如果我想知道如果我读了博士，我会走多远，这肯定是不可能的，因为时间只会向前推移。毕竟，一项实验会受到很多限制，例如，样本是否能代表整个人群，是否符合伦理等等。

**从观察数据到因果分析？**

如果进行一项实验不切实际，能否利用观测数据研究因果关系？观察数据意味着我们不能做任何干预，我们只能观察。这可能吗？

不管你懂不懂统计学，你可能听说过这样一句话，相关性并不意味着因果关系。然而，它没有告诉你如何研究因果关系。这里的好消息是，读完这本书后，你将有一个更好的框架来研究因果关系，并确定在给定数据的情况下你什么时候可以或不可以研究它，因此你知道你应该收集什么数据。

**本书的要点**

我在这里不涉及详细的技术或公式。一方面，我刚刚读完这本书，我不是因果关系的专家；另一方面，我鼓励你阅读这本书，以免错过任何见解，因为我可能会有偏见。

**尽管大数据非常突出，但将所有东西都添加到您的模型中可能是错误的**

在大数据时代，拥有几乎无限的计算能力和数据，您可能会忍不住将每个数据放入深度神经网络进行自动特征提取。我也动心了。

这本书告诉你一些场景，添加某些变量需要谨慎。例如，您想要预测 Z，而基本关系是 X →Y → Z(箭头表示“原因”，在这种情况下 Y 是一个中介，它调解从 X 到 Z 的影响)。如果你在模型中加入 X 和 Y 作为变量，Y 可能会吸收所有的“解释力”，这将 X 踢出你的模型，因为从 z 的角度来看，Y 比 X 更直接。这阻止了你研究 X 和 z 之间的因果关系。你可能会说，预测没有区别，不是吗？是的，从模型性能的角度来看，但是如果我告诉你 Y 和 Z 非常接近，以至于当你知道 Y 的时候，Z 已经发生了。

同样，不增加某些变量也是有风险的。你可能听说过伪相关或混杂这个术语。基本思想可以用这个关系式来说明，Z← X → Y(即 X 是混杂因素)。注意，Z 和 Y 之间没有因果关系，但如果不考虑 X，Z 和 Y 之间似乎有关系，一个著名的例子是巧克力消费量和诺贝尔奖得主的编号之间的正相关关系。原来共同的事业是一个国家的富裕。同样，你可能没有预测的问题，但是你可能很难向别人解释你的模型。

当然，这个世界比我们想象的要复杂。但这正是领域知识发挥作用的地方，因果图是对一切如何工作的简单而强大的表示。

书中有更高级的脑筋急转弯和现实生活中的例子。幸运的是，所提供的规则使它们易于遵循。

**因果关系可能更强**

因果关系可能会随着时间而改变。如果您希望您的模型随着时间的推移而变得健壮。以 Z← X → Y 为例，如果关系 Z← X 变弱了，对 X → Y 建模不会对你有影响，但对 Z 和 Y 建模会有影响。

从另一个角度来看，如果我们相信因果关系比关联更强，这意味着如果我们从一个领域借用到另一个领域，这种关系更有可能成立。这就是书中提到的所谓的迁移学习/可移植性。这本书引用了一个非常有见地的可移植性的例子，它描述了我们如何透明地执行调整，以便我们可以将因果关系从一个领域转移到另一个领域。

**干预变得更加容易，尤其是在数字时代**

干预实际上是研究因果关系的巨大动机之一。仅仅通过学习联想的预测模型不能给你干预的洞察力。比如不能在 Z← X → Y 中改变 Z 影响 Y，因为没有因果关系。

干预本身是一个更强大的工具，因为你可以理解潜在的关系。这意味着，你可以改变政府政策，让我们的世界变得更美好；你可以改变治疗方法来拯救更多的病人，等等..这就是你救了病人和你预测病人会死却不能干预的区别！也许这是数据科学家能做的最好的事情，只有用这个工具包！

在这个数字时代，干预需要更少的努力，当然，你有更多的数据来研究因果关系。

这是我们推理的方式，因此这可能是通向真正人工智能的途径

最后是关于人工智能。推理是智慧的必要组成部分，也是我们的感觉。在一个封闭的世界中，有明确定义的奖励和规则，强化学习通过探索和利用的平衡来实现卓越，以在预定义的规则下最大化预定义的奖励，并在所采取的行动改变状态进而决定奖励的机制下。在这个复杂的世界里，这种机制不太可能成立。

从哲学的角度来说，我们应该明白我们是如何做决定的。最有可能的是，你会问，“如果我这样做，会发生什么；如果我那样做，然后呢？”。注意，你只是创造了两个没有发生的想象世界。有时，当你反思并从错误中学习时，你可能会问，“如果我这样做了，那就不会发生了。”再说一次，你创造了你的反事实世界。事实上，我们比自己想象的更有想象力。这些想象的世界是建立在因果关系上的。

也许机器人可能有自己的逻辑，但如果我们想让它像我们一样，我们需要教它们推理。这让我想起了 DeepMind 发表的一篇论文，“测量神经网络中的抽象推理”([链接](https://deepmind.com/blog/measuring-abstract-reasoning/))，这篇论文显示了将原因作为训练数据的一部分来添加可以增强泛化能力。这篇论文让我深受启发，这正是我们教机器人推理的情况！而且是从模式联想到推理的飞跃。

我推测**因果关系有助于概括**。我没有证据，但这是我们理解世界的方式。我们被教导一两个例子，然后我们学习因果关系，我们在任何我们认为适用的地方应用这个关系。

把一切都放到一个不经意的图中，或许推理是智商测试的问答混杂因素？我们能否认为推理导致人们设计问题中的那些模式，并且它也“导致”答案？或者，它可以是一个中介，将问题转化为推理，进而导致答案？或者两者都有？请注意，我故意假设问题和答案之间没有偶然的关系，因为它们纯粹是模式关联。

![](img/8dfd2c9e31374da908a916d4efaf2902.png)

Reasoning as a Confounder

![](img/01380caf530ec9d547c0bdcc1ba90452.png)

Reasoning as a Mediator

它们只是我的胡乱猜测。我不知道答案。我不是全职研究员，也不是哲学家。但我可以肯定的是，当我们着手解决一个问题时，因果关系提供了一个新的视角。因果关系和深度学习之间的协同作用听起来很有希望。

**最终想法**

我承认这篇文章的主题可能有点咄咄逼人，但我觉得有责任向大家推荐这本书。它告诉我们因果关系的全部潜力，这是我们与生俱来的东西，但我们可能会在大数据时代忽略它。框架，do-calculus，已经存在。它只是等待我们部署并付诸实践。

作为一名从业者，有了这个强大的工具，我相信我们可以产生更好的影响。