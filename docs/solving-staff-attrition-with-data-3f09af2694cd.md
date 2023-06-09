# 用数据解决员工流失

> 原文：<https://towardsdatascience.com/solving-staff-attrition-with-data-3f09af2694cd?source=collection_archive---------3----------------------->

![](img/c475956d2e4760e1e62d0f83b5fb6979.png)

时不时地，我喜欢跳到 Kaggle 上，看看是否有我可能想玩的有趣的数据集。本周早些时候，我偶然发现了一个关于员工流失的虚构数据集。
您可以使用下面的链接找到数据集:

[](https://www.kaggle.com/ludobenistant/hr-analytics) [## 人力资源分析

### 为什么我们最优秀、最有经验的员工会过早离开？

www.kaggle.com](https://www.kaggle.com/ludobenistant/hr-analytics) 

一位名叫[卢多维克·贝尼斯坦特](https://www.kaggle.com/ludobenistant)的先生分享了这个数据集，他提出了这样一个问题:“为什么我们最优秀、最有经验的员工都过早地离开了？”
他还提出了一个挑战，那就是“享受这个数据库，并尝试预测哪些有价值的员工将会在下一个离开”，这是我肯定会做的。

然而，我必须承认，尽管他的问题很有趣，我却没有兴趣回答。我还有其他问题要问:

1.  我能预测下一个离开的员工是谁吗？
2.  我能否创建一个有助于留住员工的系统？

我承认，问题 1 离 Ludovic 想知道的并不是很远，但是我在这个实验中真正的*目标是想出一个解决问题 2 的系统。*

# 描述数据集

数据集是模拟的，包含以下字段:

*   员工满意度
*   上次评估
*   项目数量
*   平均每月小时数
*   在公司度过的时间
*   他们是否发生过工伤事故
*   他们在过去 5 年中是否有过晋升
*   部门
*   薪水
*   员工是否已经离职

# 制定方法

为了解决这个问题，我决定结合使用三种分析方法:

*   **描述性分析:**哪些观察有助于我们形成关于员工流失的各种假设？
*   **预测分析:**哪些员工将要离开？
*   **规定性分析:**对于那些可能离职的员工，你有什么见解或建议？

# 预测员工流失

只是为了好玩，我想我会先把简单的东西拿出来:建立一个机器学习模型来预测哪些员工会离开或不会离开。

我想我应该指出这种东西什么时候会在现实世界中使用。如果我在现实世界中应用这个算法，我可能会在绩效评估之后或者在“上次评估”被填充的时候运行这个算法。我认为这样做会使模型无缝地融入组织的工作流程。

对于那些可能对我的设置感到好奇的人，我正在使用一个名为 [Anaconda](https://www.continuum.io/downloads) 的 [Python](https://www.python.org/) 环境，我用它来管理我所有的包，并且我正在使用带有[和](http://deeplearning.net/software/theano/)后端的 [Keras](https://keras.io/) api 来开发我的模型。然而，我打算很快学习张量流。

对于这个任务，我创建了一个有 1 个输入层，4 个隐藏层和一个输出层的模型。准确度分数是(我很确定这里发生了一些过度拟合)。代码如下:

Neural Network Architecture for Predicting Staff Attrition

这个模型产生了 97%的准确率。

# 发展一个假设

有了创建的模型，我可以预测谁将离开组织，接下来我需要找出原因。为此，我决定使用相关性分析来确定哪些因素对员工流失影响最大。

我发现与流失最相关的变量是工作满意度，得分为 **-0.39** 。负相关意味着离职的可能性随着工作满意度的下降而增加(*有道理吧？*)。我还观察到，离开的员工比留下的员工对工作的满意度低 34%。

我有了一个良好的开端，但我还没有完全完成。

![](img/b70d592b9390c9becfbe4cbec5b6c709.png)

# 最大的问题是:什么因素有助于工作满意度？

在得知员工因为对工作不满意而离职后，我需要知道为什么会这样，以及如何提高工作满意度。为了找到解决员工工作满意度的方法，我对影响工作满意度的因素做了更深入的调查。

我做了另一个关于工作满意度的相关性分析，我发现在公司花费的时间和参与的项目数量对工作满意度的影响最大。其他因素如员工的平均月工作时间和他们最近的评估也有影响。

# 创造洞察力

现在我有了一个机器学习模型，可以预测一名员工是否会离开，我也知道什么有助于工作满意度，我需要建立一个系统，为可能很快离开的员工提供提高工作满意度的建议。我认为创建一个“保留概况”是有用的，它总结了没有离开组织的工作人员的特点。这样做将使我能够将可能离职的工作人员的概况与这一"保留概况"进行比较，并容易产生可操作的见解。

我要补充的是，如果这个系统在野外使用，我们也会考虑员工对组织的价值(这就需要回答 Ludovic 的问题)。

以下是我为创建保留配置文件而编写的代码:

现在我已经有了一个保留配置文件，下一步是创建一个系统，该系统将结合我之前创建的模型，为用户提供关于如何对待可能离开公司的员工的建议。

我想到的逻辑相当简单:

1.  使用机器学习模型来寻找可能离开组织的员工
2.  将此人的分数与之前创建的保留档案进行比较
3.  根据分数和属性与工作满意度的相关性…
4.  提出可行的建议，以提高留住人才的可能性

我得到的输出如下所示:

```
This member of staff will leave.I’ve noticed that this member of staff’s ‘number_project’ is below the norm. You may want to consider increasing his/her ‘number_project’ by 2.8155514094640495
```

我承认这不是最好看的，但我认为这是一个很好的开始。最终产品是一个**可操作的**洞察。

# 最后的想法

说明性分析有助于增强刚担任管理职位的员工的决策能力，这些员工可能正在担任此类职位或正在接受此类职位的培训。我想在某些情况下，它甚至可以用来评估这些职位的潜在候选人。

我个人认为，对于这种类型的场景，说明性分析对于找到员工不满的根本原因并找到加强员工和管理层之间关系的方法是有用的。检验这个系统是否真的能够传递价值的最好方法是在现实生活中进行尝试。

我们无法从数据中确定的一件事是组织中项目的质量，我确实相信相关性本身可能不足以确定提高工作满意度的最佳方式。也许有了更多的数据，我们可以更好地理解影响工作满意度的因素。

****更新:*** *我的一个朋友提到，这种类型的项目对于组织内各部门制定战略目标会很有用。之前没想到，但我绝对同意她的说法(感谢 Shades)。*

我希望这个实验是有用的，我希望你学到了一些东西。我在这方面很新，我会喜欢你的反馈。请尽可能诚实，建设性的批评总是受欢迎的。

这个实验的代码可以在 [**这里**](https://github.com/christfan868/staff_attrition_experiment) 找到。

如果你想知道其他人是如何处理这些数据的，请点击以下链接:

[](https://www.kaggle.com/ludobenistant/hr-analytics/kernels) [## 人力资源分析

### 为什么我们最优秀、最有经验的员工会过早离开？

www.kaggle.com](https://www.kaggle.com/ludobenistant/hr-analytics/kernels) 

其他人的想法给我留下了深刻的印象。

# 下一步是什么？

既然我已经克服了这个挑战，我将使用一个类似的数据集来测试这个方法:IBM 员工流失数据集。我想这一次我会真正回答这个问题。:)

[](https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset) [## IBM HR Analytics 员工流失和绩效

### 预测你有价值的员工的流失

www.kaggle.com](https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset) 

回头见。