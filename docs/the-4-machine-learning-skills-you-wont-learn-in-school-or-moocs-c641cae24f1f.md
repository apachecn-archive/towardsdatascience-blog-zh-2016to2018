# 你在学校或网络公开课上学不到的 4 种机器学习技能

> 原文：<https://towardsdatascience.com/the-4-machine-learning-skills-you-wont-learn-in-school-or-moocs-c641cae24f1f?source=collection_archive---------4----------------------->

![](img/0ebe373f7ab9e2bc72c1c696da61962a.png)

> 想获得灵感？快来加入我的 [**超级行情快讯**](https://www.superquotes.co/?utm_source=mediumtech&utm_medium=web&utm_campaign=sharing) 。😎

机器学习(ML)在过去几年里变得非常流行。为什么……很简单，因为它有效！最新的研究取得了破纪录的成果，甚至在一些任务上超过了人类的表现。当然，结果是许多人争先恐后地进入这个领域；为什么不呢。它资金充足，技术令人兴奋和有趣，并且有很大的增长空间。

就正规教育而言，学习机器学习有两条主要途径:学校(大学/学院)或 MOOCs(大规模开放在线课程)。正式的学校教育，比如获得硕士或博士学位，可以给你非常深入的技术和理论知识，但这也相当昂贵。MOOCs 是免费的，你肯定可以从中学习如何实际使用许多 ML 算法，尽管你不会获得通常从大学/学院获得的官方证书。然而，这两者都可以有效地用于获得在机器学习领域工作所需的技术知识。

但是…还是少了点什么。归根结底，机器学习算法正被应用于现实世界的商业问题。机器学习简单来说就是作为一个为客户创造价值的工具。这与课堂上不同，在课堂上，作业通常是单独完成的，几乎没有商业目标。重要的不仅是 ML 模型的准确性，还有它的可解释性、速度、内存消耗，以及在一天结束时，该模型如何适应产品以创造真正的价值。

今天，我将与你分享 4 种你在学校或 MOOCs 中学不到的机器学习技巧。这些都是可以通过现实世界的经验来学习的技能，使用 ML 来解决现实世界的问题并创造真正的价值。希望这篇文章能让你深入了解机器学习是如何实际应用的，以及你可以学习哪些技能来成为你所在领域的专家。

让我们开始吧！

## 将机器学习与商业目标联系起来

当你在任何涉及软件的领域工作时，包括机器学习，实际上有两个主要的理解方面:技术观点和商业观点。这两方面的知识是成为你所在领域专家的关键。

你在课堂上学到了很多技术部分。如何用 Python 编码，机器学习和数据科学算法，技术报告写作等。在课堂上，这些东西与商业是隔绝的。但是当你开始在这个领域实际工作时，你工作的每一个技术方面都与一个商业目标相关联。为什么你的老板像你一样要增加当前系统的准确性？很可能是因为更好的准确性意味着更多的价值，更多的价值意味着更好的产品，而更好的产品意味着更多的客户和金钱！

能够将这些点联系起来是很重要的，这样你就可以找到解决技术问题的最佳方法。你会知道什么是重要的部分，从而知道你应该关注什么。随着你在你的领域中资历的增加，你可能会被期望将业务目标转化为技术目标，以找到完成工作的最佳方式。技术过去是，现在仍然是用来完成更伟大事业的工具。始终考虑你的技术技能如何与商业目标相联系，以创造真正的价值。

## 型号选择

在课堂上，您将了解不同的 ML 模型。线性回归、支持向量机、决策树、神经网络……感觉有一百万个！所以最大的问题是…你用哪一个？你可能以前使用过所有这些算法，从头开始编写它们或者使用像 TensorFlow 和 Scikit Learn 这样的库。但是为什么要选择一个而不是另一个呢？现在很多人都在使用深度学习，那么我们应该默认它吗？

所有的方法都会有权衡，这就是科学和工程的本质！为了定义模型最重要的属性，将这些权衡与您的业务目标联系起来是很重要的。

一般来说，机器学习有一个被称为“没有免费的午餐”的定理，基本上是说没有一个 ML 算法对所有问题都是最好的。不同 ML 算法的性能很大程度上取决于数据的大小和结构。因此，除非我们通过简单的反复试验直接测试我们的算法，否则正确的算法选择是不清楚的。

但是，每个 ML 算法都有一些优点和缺点，我们可以用它们作为指导。虽然一种算法并不总是比另一种算法更好，但是每种算法都有一些特性，我们可以用它们来指导快速选择最佳算法并调整超参数。我也为[写了一篇关于数据科学](/selecting-the-best-machine-learning-algorithm-for-your-regression-problem-20c330bad4ef)的文章。例如，神经网络(和深度学习)通常可以达到非常高的精确度，但根本不太容易解释。当你需要确切地知道你的结果来自哪里时，使用它们可能不是一个非常好的主意；但是如果你只关心最终的输出，它们是完美的！另一方面，决策树非常容易理解，因为它们的设计非常直观。它们可能达不到深度网络所能达到的精确度，但是当你想要确切地了解你的结果来自哪里时，它们是非常有用的。

## 模型部署

机器学习教育倾向于深入到 ML 算法本身，教你它们在技术层面上如何工作。一旦您的模型完全定型，通常的做法是在一个公开的、不可见的测试数据集上测试它，以对模型性能进行基准测试。一旦我们验证了我们的模型能够很好地完成我们的任务，就必须将它部署到您为其创建模型的完整软件产品中。

从高层次来看，部署本质上涉及到将您的算法“插入”到系统的其余部分。你的模型的作用仅仅是接受一个输入，并使用它来做出某种对系统有用的预测。因此，从一个更高的层面，从系统的层面来理解你的软件是很重要的。

到目前为止，我们已经讨论了如何在学校学习非常低级的技术知识，而业务目标是定义产品价值交付的非常高级的目标。将您的软件理解为部署您的模型的连接组件的系统正好位于中间。你必须了解你的系统的架构，连接块的管道。然后，您可以将您的模型视为插入到系统中的另一个组件、块或模块。

## 让你的钱得到最大的回报

当我们在学校或参加在线课程时，我们有大把的时间去做实验。我们可以永远做研究，尝试使用最新最棒的算法，甚至尝试所有的算法来找到最好的！在现实世界中，这可能不是最有效的做事方式。

企业的时间和资源是有限的。他们不能整天尝试每一种可能的方法，看哪一种是最好的。他们需要找到高效做事的最佳方式(阅读:不浪费时间和金钱)。

你需要从物有所值的角度来看待事情。因此，也许有一种新的最先进的回归算法，但它在技术上很有挑战性，实施起来可能很耗时。与其花费如此多的时间和金钱来尝试使用它，你可能会得到更多的回报，只需为你当前的算法获取更多的数据来进行训练，或者使用最佳实践“技巧”来提高你的准确性几个点。你的算法的某些方面可能会增加大量的价值，而其他方面则不会。也许你的算法比现在更精确并不重要，但是如果它非常快，产品会有更多的价值！

在课堂上，我们很容易忽略这些事情，并且总是以某个方面的最佳表现模式为目标，忘记了我们选择的所有路径都有其权衡。关键是找出哪些权衡是值得的，哪些给你最好的回报。而且，你通常会注意到，最重要的事情与业务目标相关联。

机器学习和所有软件一般来说只是一套工具；在这种情况下，获得最大收益意味着知道如何最好地使用这些工具来完成工作。

# 喜欢学习？

在 twitter 上关注我，我会在这里发布所有最新最棒的人工智能、技术和科学！也在 [LinkedIn](https://www.linkedin.com/in/georgeseif/) 上和我联系吧！