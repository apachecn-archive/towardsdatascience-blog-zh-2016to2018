# 专家与协方差的混合

> 原文：<https://towardsdatascience.com/mixture-of-experts-with-covariance-6d4a167743ad?source=collection_archive---------4----------------------->

在这里，我将继续探索前沿的神经网络设计，以及如何使用**协方差**来改善训练时间、泛化和对新环境的适应。(我介绍了[负协方差](https://medium.com/@oaklandthinktank/overcoming-the-vanishing-gradient-problem-9569191df342)的概念，提供了[更多的](https://medium.com/towards-data-science/more-about-the-gradient-bf97e4d9c1c5) [细节](https://aboveintelligent.com/details-on-reinforcement-by-covariance-75df1d9f4725)，以及注意的背景和[可交代性](https://medium.com/towards-data-science/attention-and-explainability-in-rnns-7fd114bb4f1f)问题，在前面。)

**很复杂:**

神经网络结构正变得越来越复杂。现在，多个网络以协调的方式被使用，并且单个网络有时被分割成一个“[专家](https://arxiv.org/abs/1701.06538)”(MoE)的混合体。专家的混合使用一个非常大的神经网络中的条件路径——当信号通过网络传播时，一个*条件层*学习激活哪些专家，这样专家的各种*组合*在不同的情况下是活跃的。当这些专家中的一些决定*其他专家的参与*时，一个专家层级就形成了。因为只需要几个专家来处理每个输入，这些巨大的网络能够快速有效地处理输入，尽管它们的规模令人难以置信。

DARPA 希望制造能够边走边学的机器，这是对当前神经网络的一个重大转变，目前的神经网络首先被训练，然后被用作静态实体。要达到他们的目标，需要网络架构保留基本的识别能力，并根据新事件添加或更改解释。专家的组合可能是他们所需要的。但是，这些专家如何在旅途中学习呢？

**发展新的联系，增加专家:**

DARPA 的“终生学习者”将需要改变他们的联系，而不忘记或弄乱他们在过去学到的东西。就像我们的大脑一样，它们需要连贯地建立新的联系。不幸的是，传统的反向传播无法判断何时应该创建新的*导线*。(特别重要的是，因为训练可以产生与任何事物都没有联系的细胞！“死 ReLU”是一个常见问题。)

一个为终身学习而设计的 MoE 网络必须让现有的专家保持不变，同时让新的专家加入进来。基于协方差的强化允许网络做到这一点。

在使用来自输出层上的损失函数的反向传播来训练的网络中，没有指示新连接应该在处增长的*。然而，表现出*负协方差*的神经元可以被直接识别**(正如我在之前的[帖子](https://medium.com/towards-data-science/more-about-the-gradient-bf97e4d9c1c5)中解释的那样)，具有负协方差的神经元是**错误检测器**。当一个受过训练的 MoE 必须学习新的东西时，它可以在这些错误检测器的下游插入一个神经元集群，并将该集群训练成一个新的专家。我会更详细地解释这一点…***

****使用负协方差训练新专家:****

**当您在具有负协方差的神经元的下游插入一个神经元簇时，它们最初具有随机权重。让我们称这些星团为“noobs”。noob 可能离输出层非常远。这对于反向传播来说是一个问题，因为沿着*整个网络*的训练无法将训练集中在新的集群上。此外，额外的培训会导致现有专家的**变化，导致网络过度适应！****

**相反，您可以**冻结**网络的所有参数，**除了 noob 权重的**，并从 noob 簇*中继续呈现负协方差*的任何神经元传播梯度。(负协方差作为一个*局部*损失函数！)通过将错误分类期间的激活与网络成功期间的激活进行比较来测量负协方差。这样，*现有的*专业知识都不会丢失，整个网络*不会变得过拟合*，并且训练集中在观察到的错误上。只有新手才会学习，他们只会从错误中学习。**

****维持一个连贯的现实:****

**随着负协方差训练连续的 noobs，网络增长以容纳新的信息。noob 成为应对这些错误的专家。而且，因为负协方差是在整个网络中定义的损失函数，这些网络可以无限增长*(就像乌贼大脑……)。以这种方式发展起来的庞大网络需要一个坚实的基础。***

***那个基础，无论你的网络是执行翻译，字幕，NLP，操作机器人，设计组件，提供超分辨率，还是完成部分图像，都是 [**注定**](https://www.technologyreview.com/s/604240/a-massive-new-library-of-3-d-images-could-help-your-robot-butler-get-around-your-house/) **是 3D+时间**。***

***我们将需要一个机械土耳其人的军队:来标记 3D 物体和发生在现实的时间场景中的事件。他们还可以标记对象和事件的质量，以及关系陈述。这些标签对应于名词、动词、形容词和介词。学习这些场景片段的神经网络可以从许多角度、许多位置看到猫和自行车，它们被其他物体部分遮挡，并经历各种动作。这个 **3D+T** 模型就是*相干网络*。***

*****连贯性是基础:*****

***翻译句子时，考虑连贯网络的重要性。为了理解一个句子，*解释器*网络必须消化整个句子，它的*上下文*来自周围的句子，**和**将这个解释传递给连贯网络。如果连贯网络能够成功地*将句子实例化为现实模型*，它就声明解释者的选择是“连贯的”。这可以防止解释者犯语法上正确，但物理上*无意义的错误。****

***我们来看一个例子:“狗睡在天花板上。”*语法*没有错误发生，但是机器需要识别*:由于重力*，一只狗不能睡在天花板上。一致性网络将无法实例化该语句，并将它标记为“不一致”***

***与此同时，Coherence Network 对“猫跳到了天花板上”这一说法没有异议。物理实例化可能显示一只猫在沙发上，一路跳到天花板上。(在 youtube 上看到的；这是有可能发生的。)此外，Coherence Network 会对“狗睡在屋顶上”这种说法感到满意，因为重力允许这样做。(史努比！)***

*****与一致性网络的对话:*****

***继续解释器-示例:当解释器向连贯网络发送可能的语句时，任何不连贯的翻译都可以被抑制，并寻求二次解释，直到找到连贯的实例。如果没有找到一致的解释，网络可以用“我不确定”来回应陈述不确定性是人机交互的关键，并允许通过与人类用户的对话来学习。***

***此外，人类可以窥视连贯的网络，看看解释者在想什么。这解决了可解释性的关键问题，并允许人类用户容易地识别错误。否则，没有人知道网络是否做出了合理的判断。***

*****大图:*****

***未来的神经网络很可能是巨大的，有许多专家层的混合物。每一项新任务或特殊情况都将是这些庞大网络中的一个“耳垂”,从一个由菜鸟变成专家的层级中成长起来。企业解决方案和个性化应用程序都可以从同一个大规模网络中发展起来，*而不会增加计算成本*(因为稀疏 moe 只处理其众多路径中的[几条](https://arxiv.org/abs/1701.06538))，以及*而不需要大规模的再培训*(因为你冻结了网络的参数，并且只对错误分类的输入进行培训)。***

***最重要的是，如果你的大规模网络正在与 3D+T Coherence 网络(也被训练为 MoE with noobs)进行对话，你可以放心，它正在基于真实世界的实例找到答案，而不是随机的像素相关性。你可以看到网络在想什么，并且很容易纠正它的错误。我希望这有所帮助，国防高级研究计划局！***