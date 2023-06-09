# 关于医疗保健中机器学习的一些思考

> 原文：<https://towardsdatascience.com/some-thoughts-on-machine-learning-in-healthcare-e1cef9cec3cc?source=collection_archive---------8----------------------->

我最近在 USSOCOM 做了一个关于医疗保健中的机器学习(ML)的演讲，我想发表它以获得反馈。在 ML 任务中，找到合适的 ML 工具来克服问题和找到合适的问题来解决是不同的挑战。跨学科团队可以最好地克服这些挑战。这个博客仅限于我自己的经历，但就我的职业生涯跨越不同领域而言(协调学术 ML 研究小组，帮助深度学习初创公司，研究医学，研究商业，并在演讲系列中采访许多 ML 先驱)，我希望它带来一个广阔的视角。我可以在每个要点的基础上进行构建，并且会根据读者的反馈进行构建。

ML 在医疗保健领域的前景怎么强调都不为过。在众多承诺中，我将着重谈几个:

*   我们可以改变我们对健康的看法。被动、主动的预防医学体系让位于前瞻性预测医学和被动健康监测。
*   我们可以改变患有罕见疾病的人的生活，他们中的许多人花了十年或更长时间才得到正确的诊断，这不是因为临床医生从未听说过他们的疾病，而是因为他们在实践中从未见过它。
*   在过去的 20 年里，我们已经有了大量的临床证据，而且增长速度还在继续加快。我们正在达到一个饱和点，我们可以教人们如何遵循这些东西，即使在我离开医学的几年里，我教育的大部分领域已经过时了。ML 既可以帮助监测大量潜在信号，也可以整合最新信息，无论是来自新的临床研究还是新疾病爆发时的实时信息。

也就是说，医疗改革的步伐可能会让你失望。

*   发达国家医疗保健的激励结构是围绕下行最小化而不是上行最大化建立的。我们对临床医生的错误惩罚过度，而对他们的成功奖励过度，随着我们转向基于价值的模式，这些支出的相对规模不会发生实质性变化。因此，护理者通过尝试新的东西(尤其是新的和未经证实的)通常会获得很少或没有收获，而由于偏离护理标准而遭受重大损失。
*   我相信这就是为什么医疗保健组织倾向于不承担风险，即使给他们一些余地。以加拿大的医疗体系为例，该体系向各省提供整体拨款。这种模式的好处之一是，各省可以试验如何实施医疗保健系统，并随着时间的推移相互学习。在实践中，[试验从未体现过](https://niskanencenter.org/blog/medicaid-block-grant/)(相反，各省实施了类似的模式，并大多通过削减资金的传统政策机制来节省资金)。即使有一些力量推动医疗保健系统进行创新，这些结构内的激励因素(医疗保健工作者的职业价值观，谁得到晋升，谁受到惩罚)和围绕这些结构的激励因素(医疗事故侵权，对糟糕的医疗保健结果的负面公众反应)导致系统向平均值收敛。
*   第二，从医学的角度来说，照顾他人是“奇怪的”,而其他关系却不是。我们将这种怪异的关系正常化，将关怀行为纳入仪式中。围绕护理者的仪式在不同的民族和不同的时间有所不同，但护理总是仪式化的。我认为这是人类的需要。目前对这些仪式性角色的广泛需求将减缓医疗保健的根本变化。
*   顺便说一下，面向病人的医疗保健技术应该专注于创造这种治愈感。在吸引用户方面，创造这种治愈感可能比拥有功效更重要。看看被揭穿的补品的持久流行就知道了。
*   对于 ML 来说，转变医疗保健存在严重的技术障碍，尽管这些障碍并不是医疗保健所独有的。一些公司已经封存了大量潜在数据。很多数据都没有结构化。这种非结构化数据的保真度不是很高——一些人可能拥有完整的信息，另一些人可能没有，并且报告的信息可能会因观察者之间的差异而受到不可接受的影响。
*   以我的经验来看，在回答问题的 ML 从业者和提出这些问题的护理者之间仍然有很大的差距。我认为这部分是由于各种类型的护理人员在培训中很少接触 ML，这反过来使得 ML 研究人员更难从该领域找到合适的合作者。

如果我是一个投资者，这些将是我的论点:

*   在医疗保健的所有领域中，ML 将在未来五年对网络安全产生最显著的影响。我们已经看到对医院的网络攻击快速增长，越来越多地涉及影响患者护理和安全的勒索软件。政府对患者数据安全的重视程度非常苛刻。我预计政府将授权医院投资更好的网络安全技术。作为前兆，联邦调查局刚刚向医院发出了另一份私人行业通知(PIN ),警告他们存在网络漏洞。如果这对于政府来说是一个足够重要的优先事项，那么这将是一个要求，同时为组织购买新系统提供资金。我怀疑基于 ML 的网络安全解决方案将最适合捕捉这一价值。
*   供应链创新将*有望*对医院产生重大影响。许多在医院工作的人花费他们的时间来帮助材料流向正确的位置(例如，保持手术室供应的网络，护士一天多次给所有病人分发他们的药物)。除了无人驾驶汽车，我们正在进入一个更加无人驾驶*的时代。*
*   发展中国家将超越发达国家。在世界上的许多地方，医疗保健有一个主要的上行最大化组件。尽管我们必须在“全新护理或当前标准护理”之间做出选择，但许多人被迫选择“全新护理或不护理”，因为他们无法用现有资源满足医疗保健需求。世界上的其他地方是风险厌恶型的，技术人才是流动的，ML 的现成实现对于解决主要的医疗保健需求来说已经足够好了。求解均衡。