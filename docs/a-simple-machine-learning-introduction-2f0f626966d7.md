# 一个简单的机器学习介绍

> 原文：<https://towardsdatascience.com/a-simple-machine-learning-introduction-2f0f626966d7?source=collection_archive---------15----------------------->

当我开始学习机器学习时，我一直发现自己对自己在做什么感到困惑。在我看来，很清楚我需要编码什么，但我不明白这种编程方式与我以前开发的有什么不同。我困惑的原因是我对 ML(机器学习)的主要主题和它的基础缺乏了解。所以今天我要解释什么是机器学习的基本概念？它是用来做什么的？它的优点是什么？它有哪些应用？

机器学习是人工智能最受欢迎的分支之一。简单地说，ML 是计算机科学的一个研究领域，它研究一种特殊类型的算法，这种算法可以根据经验自动改进。换句话说，ML 算法与其他算法的不同之处在于，它们能够从我们提供给它们的数据中学习，这是 ML 如此有用的主要原因之一。在这项技术之前，软件工程师需要创建一长串规则，才能开发出能够响应我们需求的程序，但现在这种情况已经发生了变化，因为这些算法不再需要编写成千上万行代码，而是自己创建规则，以获得预期的输出。这将焦点从编码规则转移到了输入数据，使得复杂的问题相对更容易解决。

![](img/174068703d6af9cc04caf86d73cffbdd.png)

Photo by [Franki Chamaki](https://unsplash.com/photos/1K6IQsQbizI?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@franki?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

这项新技术开启了一个充满可能性和优势的世界，但它的三个主要优势是:

1)它减少了编程时间。
既然这些新算法都是要自己学习规则的，开发者就不再需要对每条规则进行显式编码，现在我们只是让算法自己学习。这方面的一个简单例子是所有提出搜索、音乐或视频建议的算法。你可以花很长时间写下每个案例，如果有人喜欢某种音乐，那么就给另一个，或者你可以制定一个算法，学习每个用户的口味，然后根据以前的数据给出建议。

**2)使产品更具可定制性和可扩展性。**
回到音乐建议的例子，想象你花了几个月的时间为你当前的市场美国创造了这个算法，但是然后你想把自己扩展到另一个国家，在那里音乐品味不同，建议不再相关。然后，你需要为这个新位置创建一个新的算法，这可能需要很长时间，但如果你使用机器学习，你可以只添加来自这个国家的数据，软件将学习如何自己提出建议，这不仅更快，而且需要更少的努力。

ML 让我们有可能解决人类无法解决的复杂问题。
有很多问题人类根本找不到确切的一套规则来使其运转。这些问题中的大多数都包含数千个可能导致结果偏差的变量，这使得对所有可能的场景进行编码变得极其困难。机器学习算法在生物科学中非常有用，这项技术使我们能够更多地了解来自身体的信号，并能够像在机器人假体中一样绘制它们。

![](img/daaf1457b571d4f92f0ea524e92432fd.png)

Photo by [Franck V.](https://unsplash.com/photos/U3sOwViXhkY?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/robotics?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在机器学习中，有不同类型的算法，这些算法分为三大类:监督学习、非监督学习和强化学习。

**监督学习**是 ML 的一个分支，其中数据被标记，换句话说，你提供给模型的信息带有答案。在这种类型的算法中，软件通过对输出进行预测，然后将其与实际答案进行比较来学习。在这种比较之后，模型的参数被调整，这个过程被称为反向传播。(我将在下一篇文章中更深入地解释这个话题)重复这个过程，直到模型能够以可接受的精度进行预测。

在**无监督学习**中，方法不同。在这种类型的算法中，数据是没有标记的，模型的目标是从数据的海洋中创建一些结构。这些类型的程序通常用于发现数据中的模式，这在商业智能中特别有用，它们利用这种模式发现能力来分析客户行为并利用这些模式。

在我看来**强化学习**是机器学习的一个非常特殊的分支，因为它非常接近人类通过试错来学习的方式。在这种类型的算法中，会创建一个性能函数来告诉模型它所做的是让它更接近目标还是让它走上另一条路。基于这个反馈，模型学习，然后做出另一个猜测，这继续发生，每个新的猜测都更好。这种类型的算法在游戏机器人中被大量使用，这些机器人一开始总是输，但渐渐地他们学会了如何在游戏中取得进展，直到他们可以比人类表现得更好。

如前所述，机器学习已经彻底改变了计算机软件的开发方式。这种算法的两个主要应用是自然语言处理(NLP)和计算机视觉。

**自然语言处理**是机器学习的一个分支，专注于让人机交互更加自然。在这里，模型的目标是在不需要某些命令的情况下理解人类想要表达的意思。这是最常用的语言翻译和聊天机器人。

**另一边的计算机视觉**正试图理解这个世界，就像我们用自己的眼睛一样。这个领域的重点是使计算机成为图像识别专家的算法。它可以从简单的算法如数字识别器到复杂的算法，如实时物体识别。

正如你所看到的，机器学习有很多应用，其中一些专注于科学，另一些专注于商业，还有一些只是娱乐，但所有这些都是有用的。这只是对这个主题的一个简单介绍，因为正如我们将在后面的文章中看到的，这个研究领域非常广泛，并且每天都在增长。

这篇文章是一系列文章的一部分，目的是为没有机器学习经验的人提供一条简单的道路。我将尽力以最简单的方式解释每个主题，同时保留该领域所有必要的主题。