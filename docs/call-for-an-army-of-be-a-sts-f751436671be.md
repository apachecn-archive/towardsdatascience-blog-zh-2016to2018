# 号召一支由法西斯组成的军队！

> 原文：<https://towardsdatascience.com/call-for-an-army-of-be-a-sts-f751436671be?source=collection_archive---------16----------------------->

## 推动一个更加民主化的人工智能。

人工智能将由三个领域提供动力，即对自然语言的更好理解，从概率分布(GANs，VAEs)中学习的生成模型，以及通过强化学习(RL)算法进行的主要成分训练。让我们来谈谈 RL，它是前进的方向，因为它学习解决问题，而不仅仅是监督算法所做的后验映射。你可以向它抛出一个下棋的问题，不管有没有你的帮助，它都会学会下棋，或者下围棋、Dota2、星际争霸，甚至是股市！

他们通过与环境互动来做到这一点，模拟你希望代理做的事情。OpenAI 和健身房一起使这个领域民主化，推动了人们的参与和对这个想法的认识。这些环境是开源力量的一个很好的例子，它是免费的，非常强大，并且有一个开发者和用户社区的支持，他们可以在瞬间解决你的问题。尽管很棒，但它缺少一个非常重要的项目，一个复杂的策略游戏，比国际象棋和其他棋盘游戏更复杂。一些有规章制度，需要大量创造力的事情。

> 尽管 OpenAI gym 很棒，但它缺少一个非常重要的项目，一个复杂的策略游戏，比国际象棋和其他棋盘游戏更复杂。

![](img/adde2936268fba2cbdd520e7a253905e.png)

A screenshot of DeepMind’s Starcraft-2 environment

如果我们看看这个领域中更多的开源项目，会发现没有什么比这更好的了。来自 [DeepMind 安全研究](https://medium.com/u/55e08ddea42e?source=post_page-----f751436671be--------------------------------)和暴雪的[星际争霸-2](https://www.wired.co.uk/article/deepmind-starchart-ai-games) 环境是开创性的，但仍然受到许多问题的困扰，不是开源的，缺乏完整版本，主要是它的大小为 30 GB！所有这些问题使得它的使用很困难。

# 那我们做一个吧

我个人在这方面已经工作了一段时间，在得到了业内一些顶尖人士的大量反馈和验证后，终于开放了。Freeciv 是一款开源的基于回合的多人深度策略游戏，有规则，这使它成为使用它作为环境的完美候选。不仅有趣，它还是人们仍然喜欢玩的最古老的游戏之一，最初的提交是在 1996 年完成的，陈旧的分支可以追溯到 21 年前！**我们正在为它编写一个 python 绑定器。**你可以在这里查看[，我们已经上传了为一篇](https://github.com/yashbonde/freeciv-python)[论文](http://groups.csail.mit.edu/rbg/code/civ/)所做的原创工作，该论文名为“通过阅读蒙特卡洛框架中的手册来学习获胜”。

![](img/61574ba6b5e5d3291df990d1f850fe2f.png)

A screenshot from freeciv 2.4

> 这项工作不仅重要，而且事后看来将是最有影响力的工作之一。这个项目不仅需要优秀的人才，还需要最优秀的人才。

有一个小团队正在努力工作，但我们需要更多的人来启动这个项目并真正建立起来。但是我们需要你的帮助。在编写代码和动态环境方面需要做大量的工作。我们从一个简单的需求开始，编译源代码并记录这个过程。最终目标是创造一个智能体，它可以在人类最少的帮助下(唯一的支持应该是基本的指令)学会自己在复杂的环境中穿行和玩耍。

# 在这里应用深度强化学习

这个环境将为测试人工智能提供一个巨大的机会，因为以下原因，你也可以把这作为我们需要在这个项目中实现和贡献的事情的宣言:

1.  **开放式奖励结构:**由于可以采取如此多样的游戏产品和行动，用户将获得原始信息，如果他们愿意，可以编写自己的奖励结构，尽管我们将提供基本奖励。最近大多数突破性的模型都应用了元学习风格的体系结构，具有自动奖励理解。这种环境将推动这一进程更上一层楼。
2.  **深层次结构:**游戏需要做的事情太多了，这就要求代理对各个层次应该做什么有更深的理解，而不仅仅是看一下画面就决定下一步的行动。
3.  **长期游戏性:**由于游戏可以持续许多回合，它需要代理人进行非常长期的战略思维处理。比现在任何环境都要长，也更多样化。
4.  **信息类型:**游戏不只是发送一个原始图像，而且其中许多，代理得到各种各样的地图(资源，单位，财产)而不是一个单一的图像。文本中有规则和规定，许多策略指南，使你的模型能够处理不同类型的信息，我们人类认为这些是理所当然的。
5.  **一般智能:**游戏中的多样性、结构和要做出的决定是如此开放和广阔，以至于你的代理人(或全体)需要有一个非常一般的思维过程。这种平台将导致研究和代理，这将使我们对人工智能的理解和发展更好。
6.  **大小:**目前最大的优势是大小，一个全功能的互动游戏不到 100MB，游戏中有 API 的源代码，所以你可以记录你的动作，然后用它们来训练你的模型。
7.  **【奖金】小游戏:**为了让初学者更容易开始这方面的工作，我们旨在发布各种各样的小游戏，就像星际争霸 2 中的环境一样，这将帮助你在进入主游戏之前测试你的模型到简单的任务。

![](img/9c2807c8ca12363cd790dc5ff207d86c.png)

Let’s not be this dumb

**这一切都是这个环境所提供的；主要的困难是，我们需要建造并测试这个东西。**回购是新的，项目将被添加到其中，以指导我们并为项目设定基准。

github 回购链接:[https://github.com/yashbonde/freeciv-python](https://github.com/yashbonde/freeciv-python)

欢迎贡献者，如果你有任何疑问/想法，请打我的 LinkedIn 联系我，我不介意现在是凌晨 4 点，我会回复你。

干杯！