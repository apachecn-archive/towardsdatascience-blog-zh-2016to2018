# 真实的数据科学

> 原文：<https://towardsdatascience.com/data-science-for-real-c09f088b6550?source=collection_archive---------9----------------------->

![](img/e2fe9833b5d20252b89137727ebef3cf.png)

# 借助高级分析和机器学习实现物业管理转型

> “它是有形的，它是坚实的，它是美丽的。从我的角度来看，这是艺术，我就是喜欢房地产。”- 唐纳德·特朗普

我通常不同意特朗普总统的观点。事实上，恰恰相反。尽管——关于房地产——我们似乎有共同的爱好。

几千年来，房地产一直是财富的代名词，帮助人们积累了大量财富，未来几代人可能还会继续如此。通过房地产投资创造价值的一个关键因素是健全的物业管理。

虽然已经开发了久经考验的财产管理技术，但其中许多方法是在模拟世界中开发的。我们现在生活在一个设备变得越来越智能、万物互联、算法正在抢走我们工作的时代。我们已经从模拟转向数字。在这个新的数字时代，物业经理仍然扮演着重要的角色，但我们现在越来越有能力让他更有效率，让他把时间花在对业务有更大影响的任务上。

房地产公司可以通过多种方式利用数据科学来改善物业管理——从集成智能建筑技术到为租户管理实施机器学习模型。本文将讨论为使用这些技术做准备的一些方法，并展示高级分析和机器学习模型在物业管理中的具体用例。

# 跑之前先走

使用机器学习算法来推动利润听起来很酷——它可能是价值的巨大驱动力，但在这些技术能够得到充分利用之前，需要对业务流程、结构和治理有所了解。

## 过程

首先，应该清楚地理解和定义业务流程。业务流程管理，或者被从业者称为 BPM，可能已经过时了，但是仍然可以从绘制流程图和分析流程中获得有价值的见解。BPM 可以清楚地了解当前的流程，并且更容易看到流程的哪些部分可以用新技术改进，哪些应该保持原样。对您的流程采用模块化方法，并分析每个步骤中所需的输入和输出。始终考虑简化和标准化的方法，因为这将使数字化和自动化更加容易。

## 从电子表格到数据库

像微软的 Excel 这样的电子表格程序取得了巨大的成功。它们被世界上数百万的企业所使用，对于许多特殊的任务，它们表现得非常好。但当涉及到报告和更高级的任务时，电子表格可能会很麻烦，容易出错，并且无法提供模型所需的正确数据。当然，您可以通过集成 Visual Basic 代码使您的工作表变得智能，并创建伟大的宏，但这可能很难开发出一个潜在的噩梦来维护。

就其本质而言，易于操作和更改，电子表格并不是报告和其他日常任务的理想解决方案。这几乎肯定会导致错误和模糊性的增加。从电子表格转向更像数据库的世界，使得机器学习算法更有效地应用于问题成为可能。在一个更加结构化的系统中，任务可以被更大程度地分析和自动化。这对于想要涉足数据科学的公司来说至关重要。

## 数据治理

如何处理数据，如何保护和存储数据，谁可以插入、更新或删除记录，这些都是数据治理中的关键问题。企业从数据治理中受益，因为它有助于确保数据的一致性和可信性，并符合法规约束。

从数据科学的角度来看，数据的质量和一致性至关重要。老话“垃圾进，垃圾出”在训练和使用机器学习模型时尤其适用。没有好的数据，模型会变得更弱，它们的输出和预测会变得不可信。因此，强烈建议在实施高级机器学习项目之前，建立一个良好的数据治理流程。

# 使用数据科学

有了正确的流程、数据治理和架构支持，现在是时候在数字化之旅中勇往直前了。数据科学——将高级分析和机器学习模型应用于行业问题——是下一个自然的步骤。下面是几个例子，说明如何利用这项技术来加强物业管理。

## 租户流失

客户流失建模是数据科学的经典应用之一。几十年来，银行、保险和电信等行业一直使用客户流失模型来预测客户行为，它在物业管理方面也有明显的用例。

在其最简单的形式中，流失模型是一个二元分类模型，给定一组预测值或输入变量，输出一个分类。例如，如果租户租用一个单元，流失模型可以用来预测租户在给定的时间范围内(例如 1 年)离开的概率。

有了这些知识，物业经理可以更好地了解租户组合将如何随着时间的推移而变化，以及哪些单元可能会很快可用。这将使经理能够主动锁定高流失率的候选人，并为他们延长合同提供激励。此外，该模型可以突出哪些单元可能需要在未来被填充，从而可以减少单元的空缺期。

流失模型也可以有效地用作大型预测模型的组件，其中流失的概率被纳入未来现金流，并在广泛的租户群体中进行汇总。通过这样做，一家房地产公司可以对其现金流做出更准确的预测，从而在不增加风险的情况下增加其总杠杆。最终，导致更有效地利用资本。

房地产公司认真对待租户管理的一个例子是 Spire 物业管理。他们使用 MRI(一种专用的房地产软件解决方案)来帮助防止客户流失。据 Spire 的执行董事肖恩·保罗称，他们使用 MRI 来“简化客户关系管理……组织、自动化和评估其保留工作——跟踪租赁和租赁周年纪念、租户记录、维护活动和工作订单”。有效地为物业管理公司和租户创造双赢的解决方案。

## 为新租户带来商机

你知道谁是你最好的房客吗？他们是有最高支付意愿和能力的人，还是那些总是延迟支付以便你可以收取滞纳金的人？或者，最好的租户可能是一至两年周转期短的租户，这让你有机会签订新合同并提高租金。这个问题的答案无法通过机器学习模型来回答，而是应该从商业角度进行评估，与公司的整体战略保持一致。

一旦明确定义了最佳租户，并且公司知道它想要谁作为租户——请记住，这可能因建筑而异——就有可能使用机器学习算法来绘制出这些理想租户的特征。然后，可以在各种潜在客户列表中运行该功能集，以确定哪些客户有可能成为最佳租户。当特征集丰富而复杂时，机器学习模型通常在超人的水平上执行这种类型的分类，并且比人类好得多。

对于商业房地产，也有一些供应商帮助公司产生线索，增加销售。Vainu 就是这种公司的一个例子。他们成立于 2013 年，正在使用机器学习模型和大型数据库来辅助销售过程。房地产公司 Technopolis 的一项案例研究显示，与以前相比，他们在销售机会挖掘方面所用的时间减少了三分之一。这种类型的解决方案可能特别适用于希望增加其商业单位销售线索的物业经理。

## 员工的位置优化

考虑下面的场景。一家公司拥有两栋带有几个单元的办公楼，并且有员工使用这两栋楼。由于意想不到的情况，办公空间的使用出现了不平衡，导致一栋建筑超负荷使用，而另一栋却未得到充分利用。这种次优情况如何用技术改善？

使用分析和传感器系统，可以监控员工的位置，并且可以配置自动消息系统来通知员工不平衡，并引导该组的子集到较少占用的空间。这种类型的优化工作实施起来并不困难，但如果经常出现不平衡，可以节省大量资金，并可以减少办公空间的总体使用量。

## 智能建筑技术

智能建筑技术有望让物业经理受益匪浅。有些创新相当新，它们的潜力还没有完全发掘出来，但有几个用例非常突出。

**预测性维护**

预测性维护可以帮助您在建筑物出现问题之前发现问题，从而采取措施防止故障或限制维修造成的停机时间。这可以使维护人员更加有效，从而降低成本，并可能增加设备的总寿命。对于租户来说，缩短关键基础架构维修的停机时间也是有利的。

使用预测性维护技术的第一步是为需要监控的设备添加传感器。来自这些传感器的数据然后被收集在数据库中，并且在操作一段时间后，关于系统操作的时间序列数据被累积。假设我们有足够的观察结果，那么时间序列就包含了建立预测系统下一次故障的机器学习模型所需的数据。

这些机器学习模型通常是分类模型或回归模型。在分类模型的情况下，我们将尝试预测在接下来的 n 个时间步骤内失败的概率。通过回归模型，我们可以预测下一次故障之前还剩多少时间，这通常被称为“剩余使用寿命”。无论选择哪种模型，都将取决于系统的类型和建模可用的数据。

**建筑信息建模**

建筑信息建模，简称 BIM，是智能建筑领域的另一项激动人心的技术发展。基本的想法是，该建筑有一个完全相同的数字孪生与示意图和三维模型。虽然许多建筑公司使用 BIM 来帮助他们的建筑过程，但他们也可以在物业的生命周期内提供显著的优势，从而帮助物业经理。

BIM 对物业管理有用的一个典型例子是当建筑中的系统出现故障时。由于建筑本身具有完整的 3D 模型，维护工程师可以在穿越建筑时使用增强现实，并在进行维修时获得关键的建筑信息。可以提供给工程师的数据包括服务历史记录、系统规格和合同信息，使维修过程更容易、更快，并且与预测性维护一样，还可以缩短关键基础设施的停机时间。

# 超越物业管理

值得注意的是，我们主要讨论了如何利用数字化和数据科学来改善物业管理。这当然只是房地产行业的一个子集，对于整个行业来说，数据科学还有很多其他可能的应用领域。机器学习模型现在被用来预测从价格和租金收入到人口趋势的任何事情。随着我们继续使用更多的物联网设备和算法变得更好，我们肯定会看到更多的用例发展。

通过使用新兴的数字技术，有许多方法可以加强物业管理。但是，为了充分利用分析和机器学习方面的最新进展，一个组织需要一定程度的数字成熟度。然而，一旦达到这个阈值，数据科学就可以以多种方式使用。通过更好地了解租户及其流失情况，或者通过使用预测性维护技术和 BIM 模型，可以节省成本，通过销售线索挖掘模型可以增加销售额。

如果您喜欢这篇文章，并希望看到我的更多内容，或者希望使用我的服务，请随时在 https://www.linkedin.com/in/hans-christian-ekne-1760a259/[的 LinkedIn 上与我联系，或者访问我在 https://ekneconsulting.com/](https://www.linkedin.com/in/hans-christian-ekne-1760a259/)[的网页，查看我提供的一些服务。如有任何其他问题或意见，请发邮件至](https://ekneconsulting.com/)[hce@ekneconsulting.com](mailto:hce@ekneconsulting.com)给我。

感谢阅读！

参考资料:

 [## 磁共振成像软件-解放你的房地产业务

### MRI 软件提供创新的房地产解决方案，解放您的公司。了解我们的开放和互联…

www.mrisoftware.com](https://www.mrisoftware.com/) [](http://www.bizcommunity.com/Article/196/567/158822.html) [## 租户流失会如何影响盈利能力

### 租户，作为商业建筑的主要收入来源，是关键，因此租户保留应该是首要的…

www.bizcommunity.com](http://www.bizcommunity.com/Article/196/567/158822.html) [](https://www.infoq.com/articles/machine-learning-techniques-predictive-maintenance) [## 预测性维护的机器学习技术

### 在这篇文章中，作者探讨了如何建立一个机器学习模型来进行系统的预测性维护…

www.infoq.com](https://www.infoq.com/articles/machine-learning-techniques-predictive-maintenance) [](https://searchdatamanagement.techtarget.com/definition/data-governance) [## 什么是数据治理(DG)？-WhatIs.com 的定义

### 数据治理(DG)是对数据的可用性、可用性、完整性和安全性的全面管理…

searchdatamanagement.techtarget.com](https://searchdatamanagement.techtarget.com/definition/data-governance) [](https://www.autodesk.com/solutions/bim) [## 什么是 BIM |建筑信息建模| Autodesk

### BIM(建筑信息建模)是一个智能的三维模型为基础的过程，给建筑，工程和…

www.autodesk.com](https://www.autodesk.com/solutions/bim)