# 分析数据的常见模式

> 原文：<https://towardsdatascience.com/common-patterns-for-analyzing-data-da1908640641?source=collection_archive---------7----------------------->

![](img/bfb34e7bbe7132b5f97abd941aa64230.png)

Photo by [Samuel Zeller](https://unsplash.com/photos/hWUiawiCO_Y?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

数据通常是杂乱的，建立准确模型的关键步骤是彻底理解您正在处理的数据。

在我几个月前开始自学机器学习之前，我没有太多考虑如何理解数据。我假设数据是放在一个很好的有组织的包中，顶部有一个蝴蝶结，或者至少有一套清晰的步骤可以遵循。

通过查看其他人的代码，我对人们理解、可视化和分析相同数据集的方式的差异感到震惊。我决定通读几种不同的数据分析，试图找到相似之处和不同之处，看看我是否能**提炼出一套理解数据集的最佳实践或策略，以便最好地利用它们进行分析**。

> 数据科学家将大部分时间花在数据准备上，而不是模型优化上。— [洛林克](https://www.kaggle.com/lorinc/feature-extraction-from-images)

在这篇文章中，我选择了一些在数据科学网站 [Kaggle](https://www.kaggle.com/) 上公开的 [**探索性数据分析**(或 EDAs)](https://www.kaggle.com/general/12796) 。这些分析将交互式代码片段与散文混合在一起，可以帮助提供数据的鸟瞰图或梳理出数据中的模式。

我同时研究了[特征工程](https://www.quora.com/Does-deep-learning-reduce-the-importance-of-feature-engineering)，这是一种获取现有数据并以赋予额外含义的方式对其进行转换的技术(例如，获取时间戳并提取一个`DAY_OF_WEEK`列，这可能会在预测商店销售额时派上用场)。

我想看各种不同种类的数据集，所以我选择了:

*   结构数据
*   自然语言
*   图像

请随意跳到下面的结论，或者继续阅读深入研究数据集。

## 标准

对于每个类别，我选择了两个已经过了提交日期的比赛，并根据提交的团队数量进行了排序。

对于每一场比赛我都搜索了 EDA 标签，选择了三个评价很高或者评论很好的内核。最终分数没有考虑在内(一些 EDA 甚至没有提交分数)。

# 结构数据

结构化数据集的特征在于包含训练和测试数据的电子表格。电子表格可能包含分类变量(颜色，如`green`、`red`和`blue`)、连续变量(年龄，如`4`、`15`和`67`)和顺序变量(教育水平，如`elementary`、`high school`、`college`)。

> **插补** —填充数据中缺失的值
> 
> **宁滨** —将连续数据组合成桶，一种特征工程的形式

训练电子表格有一个您试图求解的目标列，它将在测试数据中丢失。我检查的大多数 EDA 都集中在梳理目标变量和其他列之间的潜在相关性。

因为你主要是在寻找不同变量之间的相关性，所以你可以分割数据的方法就只有这么多。对于可视化，有更多的选择，但即使如此，[一些技术似乎比其他技术更适合手头的任务](/5-quick-and-easy-data-visualizations-in-python-with-code-a2284bae952f)，导致了许多看起来相似的笔记本。

你可以真正发挥想象力的地方是特性工程。我看到的每个作者都有不同的特征工程方法，无论是选择如何绑定一个特征还是将分类特征组合成新的特征。

我们再来深入看两个比赛，[泰坦尼克号比赛](https://www.kaggle.com/c/titanic)，其次是[房价比赛](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)。

## 泰坦尼克号

泰坦尼克号比赛是一项很受欢迎的初学者比赛，许多 Kaggle 上的人都参加了这项比赛。因此，EDA 往往写得很好，记录得很完整，是我见过的最清晰的。该数据集包括一个训练电子表格，其中有一列`Survived`指示乘客是否幸存，以及其他补充数据，如他们的年龄、性别、机票价格等。

我选择分析的 EDA 是 *I 的[EDA to predict Dietanic](https://www.kaggle.com/ash316/eda-to-prediction-dietanic)，Coder* ， [Titanic Survival for 初学者 EDA to ML](https://www.kaggle.com/dejavu23/titanic-survival-for-beginners-eda-to-ml) 的 *deja vu* 和[In Depth visualization Simple Methods](https://www.kaggle.com/jkokatjuhha/in-depth-visualisations-simple-methods)Jekaterina Kokatjuhha。

所有三个 EDA 都从原始指标开始，查看几个样本行并打印关于 CSV 文件的描述性信息，如列的类型、平均值和中值。

![](img/58ffdeb153dfea9ff3bfce4a1d6fc153.png)

I, Coder describes the dataset

处理空值或缺失值是数据准备的关键步骤。一个 EDA 直接处理这个问题，而另外两个在特性工程阶段处理缺失值。

*我，编码员*反对分配一个随机数来填充缺失的年龄:

> 正如我们之前看到的，年龄特性有 177 个空值。为了替换这些 NaN 值，我们可以为它们分配数据集的平均年龄。但问题是，有很多不同年龄的人。我们不能给一个 4 岁的孩子分配 29 岁的平均年龄。有什么办法可以查出这位乘客属于哪个年龄段吗？？答对了。！！！，我们可以检查名称功能。查看该特征，我们可以看到姓名带有称呼，如 Mr 或 Mrs。因此，我们可以将 Mr 和 Mrs 的平均值分配给相应的组。

![](img/2fd4814f7c43cacb14f9165037c58b9c.png)

*I, Coder* imputing ages

虽然 *I，Coder* 将特征工程作为纯数据分析的一部分，但其他两位作者认为这是一个独立的步骤。

所有三位内核作者都非常依赖图表和可视化来获得对数据的高层次理解，并找到潜在的相关性。使用的图表包括因子图、交叉表、条形图和饼图、小提琴图等。

![](img/2bb6498b0f12faafd251c1ff719b7a7a.png)

deja vu plots survival by gender

你可能对泰坦尼克号灾难中的“妇女和儿童优先”这句话很熟悉，对于每个作者来说，年龄和性别在他们最初的数据分析中占了很大比重。收入背景(如机票价格所示)也需要进行一些详细的检查。

> 船上男人的数量比女人的数量多得多。然而，获救的女性人数几乎是男性人数的两倍。船上女性的存活率约为 75%,而男性约为 18-19%。—我，编码员

*杰卡特琳娜*和*本人、编码员*都是通过对图表和数据的目测得出结论，其中*杰卡特琳娜*写道:

*   性:女性生存几率更高。
*   有一张头等舱机票对生存是有益的。
*   SibSp 和 Parch:中型家庭比独自旅行或大家庭的人有更高的存活率。原因可能是，只有人们愿意牺牲自己来帮助别人。关于大家庭，我会解释说，很难管理整个家庭，因此人们会在上船之前寻找家庭成员。
*   登船 C 的存活率更高。例如，看看 Pclass 1 的大部分是否在 embarked C 中出现，这将是很有趣的。

![](img/fad24c1516b328f8c8cd51460d83ca7f.png)

Jekaterina builds a stacked chart illustrating Pclass and Embarked

*似曾相识*的 EDA 记录了他分析的每一步的准确度，提供了一个很好的反馈，说明每个特征对最终预测有多重要。

## 特征工程

![](img/baed8a77c5ff563417d07ce27966c34d.png)

Jekaterina pulls out cabin letter.

谈到特性工程，三个内核作者之间有更多的可变性。

每位作者为年龄和费用等连续变量选择不同数量的桶。与此同时，每个人都以不同的方式处理家庭关系，其中 *I，编码者*建立了一个`SibSip`——无论一个人是独自还是与家人(配偶或兄弟姐妹)——以及`family_size`和`alone`，而*杰卡特琳娜*拿出一个小屋，并为`child`或`adult`建议一个功能。*我，编码员*在剔除不相关的列时特别积极:

> Name →我们不需要 Name 特性，因为它不能被转换成任何分类值。
> 
> 年龄→我们有年龄带功能，所以不需要这个。
> 
> 票→是任意一个无法分类的随机字符串。
> 
> Fare →我们有 Fare_cat 特性，所以不需要
> 
> 客舱→许多 NaN 值以及许多乘客有多个客舱。所以这是一个没用的功能。
> 
> Fare_Range →我们有 fare_cat 功能。
> 
> PassengerId →无法分类。

对于插补步骤， *Jekaterina* 写道:

*   上船:用大船装满船
*   Pclass:因为 Fare 中只有一个缺失值，所以我们将用相应 Pclass 的中间值来填充它
*   年龄:有几种输入技术，我们将使用范围均值+-标准差中的随机数

她通过确保新的估算数据不会扰乱均值来总结她的内核:

![](img/ffb1c4ae256eb442cb0647cf508d3269.png)

Jekaterina checking if the imputation disrupted the mean

## 外卖食品

所有三个内核作者都花时间预先检查数据并描述整体形状。

*I，Coder* 查看总的空值，而 *Jekaterina* 在接近结束时查看。

每个人都从查看幸存者的分类开始，然后是幸存者按性别的分类。交叉表、因子图和小提琴图都是流行的图表。Jekaterina 还绘制了一些非常有趣的图表。

当谈到特征工程时，作者们的分歧就更大了。作者们在何时设计新功能的问题上意见不一，一些人将其视为一个独立的步骤，而另一些人则在他们对数据的初步分析中处理它。宁滨各地的选择各不相同，年龄、头衔和费用都有不同数量的桶，只有*杰卡特琳娜*设计了一个离散的`child` / `adult`特征。

估算的方法也不同。 *I，编码员*建议查看现有数据来预测插补值，而 *Jekaterina* 确保她的插补数据不会影响平均值。

两位作者在思考和处理数据的方式上有一些明显的相似之处，主要分歧在于可视化和特征工程。

## [房价](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)

![](img/f66df71fe328ecde379d72129010cf2c.png)

by [American Advisors Group](https://www.flickr.com/photos/120360673@N04/13855784355/in/photolist-n7ovXH-gjrMhS-eDwNQx-fFyccW-eDCzpL-fQDNaP-cA4RYd-cA4MtL-cA4HuL-fKnTsf-cA4LzU-ssvhf2-fKnAV9-daEeEz-gtpvp8-cA4R5o-cA4XQ7-cA4NSA-g2hXow-cA4SQw-eDBSFb-9eW1ng-g2j9Z5-cA4xwN-fFyJkx-9EzH9a-UD524Z-gttD2c-v9HAST-R7GoBF-v9KGVk-irUqRZ-koMrNT-fKv1e1-cA4UCE-ggDSAS-cA4C4A-gi21pE-cA4wdd-qmiDzR-rSUbew-gnDV6V-gjucTQ-fK7FS6-fK7bD6-duD885-fKbUqP-ggrui7-DUB1dh-dsvoVH)

[房价](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)又是一场结构化数据竞赛。这一项比泰坦尼克号竞赛拥有更多的变量，包括分类、顺序和连续特征。

我选择分析的 EDA 分别是*佩德罗·马塞利诺*的[用 Python 进行的](https://www.kaggle.com/pmarcelino/comprehensive-data-exploration-with-python)全面数据探索、*安吉拉*的[用 Python 进行的](https://www.kaggle.com/xchmiao/detailed-data-exploration-in-python)详细数据探索，以及*尚贤公园*的[趣味 Python EDA 一步步](https://www.kaggle.com/caicell/fun-python-eda-step-by-step)。

虽然类似于泰坦尼克号，但它要复杂得多。

> 有 79 个解释变量描述了(几乎)爱荷华州埃姆斯住宅的每个方面，这个比赛挑战你预测每个家庭的最终价格。

![](img/e9776d5cc28187254f1ceed4a85f68d5.png)

Pedro plots the sale price

安吉拉和佩德罗花了一些时间预先调查初始数据，就像我们在《泰坦尼克号》中看到的那样。 *Angela* 在直方图中绘制销售价格并构建功能热图，而 *Pedro* 绘制销售价格并得出以下关于销售价格的结论:

> *偏离正态分布。
> 
> *具有明显的正偏度。
> 
> *显示峰值。

*佩德罗*然后站在买家的角度，推测哪些功能对他很重要，检查他的选择和销售价格之间的相关性。后来，他构建了一个热图，在放大几个有希望的候选人之前，收集更客观的特征关系视图。

![](img/9459aecc7ca283b10e32d5ce4f69866e.png)

Plotting features against sale price

相比之下，*安吉拉*从更客观的方法开始，通过与`SalePrice`的相关性列出数字特征。她还根据销售价格绘制特征图，寻找数据中的模式。

*Sang-eon* 开始他的内核，积极剔除缺失值和离群值(除了`LotFrontage`他使用线性回归估算)。只有到那时，他才开始针对销售价格策划各种特征。

*Pedro* 一直等到寻找数据之间的相关性，以检查缺失数据的问题。他问道:

*   缺失数据有多普遍？
*   缺失数据是随机的还是有规律的？

> 由于实际原因，这些问题的答案很重要，因为缺失数据可能意味着样本量的减少。这可能会阻止我们继续进行分析。此外，从实质性的角度来看，我们需要确保缺失数据的处理过程不会有偏见，不会隐藏一个难以忽视的事实。

为了解决这些问题， *Pedro* 绘制了缺失单元格的总数和百分比，并选择删除 15%或更多单元格包含缺失数据的列。他再次依靠主观选择来确定要移除哪些特征:

> …我们会错过这些数据吗？我不这么认为。这些变量似乎都不是很重要，因为大部分都不是我们买房时考虑的方面(也许这就是数据缺失的原因？).此外，仔细观察变量，我们可以说像' PoolQC '，' MiscFeature '和' FireplaceQu '这样的变量是离群值的强候选，所以我们很乐意删除它们。

*Pedro 处理缺失数据的*方法是，如果列(特征)具有大量缺失值，则完全删除它们，或者删除只有少量缺失值的行。他没有估算任何变量。他还建立了一种解决异常值的启发式方法:

> 这里主要关心的是建立一个阈值，将一个观察定义为异常值。为此，我们将对数据进行标准化。在这种情况下，数据标准化意味着将数据值转换为平均值为 0，标准差为 1。

他的结论是，从统计的角度来看没有什么可担心的，但是在返回到数据的视觉检查之后，删除了一些他认为有问题的单个数据点。

## 特征工程

*Sang-eon* 检查数据的偏斜度和峰度，并执行 Wilxoc-秩和检验。他以一个非常好看的情节结束了他的内核:

![](img/87779479fd04338e5e7ce35e035b4f02.png)

Sang-eon with a 3d plot of features

同时， *Pedro* 讨论了正态性、同方差性、线性和不存在相关误差；他将数据标准化，发现其他三个问题也解决了。成功！

## 外卖食品

三个内核作者都没有做太多的特性工程，可能是因为数据集中已经存在太多的特性。

有各种各样的策略来确定如何处理数据，一些作者采用主观策略，而另一些作者则直接采用更客观的测量方法。对于何时以及如何剔除缺失值或异常值，也没有明确的共识。

与《泰坦尼克号》比赛相比，这里更注重统计方法和整体的完整性，可能是因为有太多的功能需要处理；与之前的比赛相比，负面的统计效应可能会产生更大的整体影响。

# 自然语言

自然语言(NLP)数据集包含单词或句子。虽然核心数据类型与结构化数据竞赛中的相同，即文本，但可用于分析自然语言的工具是专门的，导致了不同的分析策略。

在原始形式下，语言不容易被机器学习模型破译。要将其转换成适合神经网络的格式，需要进行转换。一种流行的技术是[单词包](https://en.wikipedia.org/wiki/Bag-of-words_model)，通过这种技术，一个句子被有效地转换成 0 或 1 的集合，以指示某个特定单词是否存在。

由于需要转换数据，大多数笔记本的前几个步骤往往是将文本转换成机器可读的东西，这一步在笔记本之间往往是相似的。一旦完成了这些，编码人员在他们的方法上就有了很大的分歧，并为特性工程采用了各种不同的可视化和技术。

## [毒性评论分类](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge)

警告:这些评论中的一些可能会灼伤你的眼球。

![](img/79f16b88c3f0142c389053532a9d715e.png)

by [navaneethkn](https://www.flickr.com/photos/navaneethkn/7975953800/in/photolist-d9NRbQ-dEZp2L-dQinfV-8ZqMDd-GyaoHJ-oGKC67-5Kj4pp-8YybhA-8Yva5t-7Xh81B-oEZ6w8-4G19MZ-cm3zDf-3c7z32-GXuYz-oyayD-96qUSC-6UYVbr-bjWoro-duyWt-7jD4Nc-6KNazu-op1rhC-DY1c6F-bYNV7U-byHgQ3-cmFxgG-cm3zEC-8m74XJ-oZEcpA-9Kd3gM-7t1H1q-m9ZbHK-9r7F3j-r3kU-8ZPcAU-8RLfw5-TsHmuW-98S9zG-8Mzx2B-c6ZoZ9-7Bpck-8bnj49-4AJUnS-vag3VE-7Bp97-jeiiRG-bHbYQa-dJQMhT-N7SSSy)

我关注的第一个 NLP 竞赛是[有毒评论分类竞赛](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge%3CPaste%3E)，它包括一个数据集，其中包含大量来自维基百科 talk page edits 的评论，这些评论按照毒性等级进行评分，表明它们是否是侮辱、淫秽、有毒等等。挑战在于预测给定评论的毒性标签。

我选择分析的 EDA 是 [Stop the S@#$ —有毒评论 EDA](https://www.kaggle.com/jagangupta/stop-the-s-toxic-comments-eda) 作者*贾根*、[分类多标签评论](https://www.kaggle.com/rhodiumbeng/classifying-multi-label-comments-0-9741-lb)作者*铑 Beng* 和[不要惹我母亲](https://www.kaggle.com/fcostartistican/don-t-mess-with-my-mothjer)作者*弗朗西斯科门德斯*。

三位作者都是从描述数据集开始，并随机抽取一些评论。虽然没有丢失值，但是注释中有很多干扰，但是不清楚这些干扰在最终的数据分析中是否有用。

![](img/33c8bf89c98fecc3c94434c9ed16f1be.png)

Jagan plots the distribution of images per toxic category

> 毒性并没有在各个阶层中均匀分布。因此，我们可能会面临阶级失衡的问题

*Francisco* 立即扔掉“缺乏意义”的单词(例如，“and”或“the”)。利用双标图，他画出一个特定的单词最有可能属于哪一类。

> 从 biplot 来看，大多数单词都像预期的那样组织起来，除了一些例外，fat 与身份仇恨有关，这令人惊讶，因为它是图表底部唯一的非种族单词，在图表中间有一些通用的攻击性单词，这意味着它们可以用于任何可怕的目的， 其他像 die 这样的单词只与威胁相关联，这完全说得通。其他一些像$$(抱歉，我写它时感觉不舒服，因为它出现在数据上)与威胁相关联，在图表的左中部有一些无法识别的单词，这些单词使用代码显示——Francisco Mendez

Francisco 接着询问拼写错误和毒性之间是否存在关联。

> 显然是有的，令人惊讶的是，拼错的 mother 与仇恨或威胁无关，但当拼写正确时，会有一些仇恨和威胁评论中有 mother 这个词…这是因为人们在威胁某人或讨厌它时会写得更仔细吗？

随着 Francisco 的深入研究，他发现在许多情况下，有害的评论会一遍又一遍地包含复制粘贴的短语。在删除重复的单词后，他重新进行分析，发现了一组新的相关性。

> 这里有一些新词，可能是 gay，主要用于威胁性评论和仇恨。一些一般温和的词，如母亲，地狱，一块，愚蠢，白痴和关闭被用于任何有毒的一般目的，同时任何衍生的 f 字被用于有毒和淫秽的评论。此外，从双标可以认识到，毒性和侮辱是相似的，是最不具攻击性的，而仇恨和威胁是最严重的。

这三位作者都充分利用了数据的可视化效果。(鉴于主题我[不会嵌入](https://www.kaggleusercontent.com/kf/1999919/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..VNoIJq1HAQhUsgxohTIQbw.PJ_2btsXr_QE8M47LbU_hnDC0EjxjMc2MU78sA3FgRImN8RkF7EHKV3qblwpWNMFxd1euS-fJoKYaH08WmK_WrOThoricdI7DSnR_bPBpbcYd38Ee2nI79hiLFLmfOYqvouAokDBWFJttLZ1hNABug.HeaSlJMn0s2ZxykWFP8wPg/__results__.html#Counting-words-different)图片[，但是你可以在每个作者的内核](https://www.kaggleusercontent.com/kf/2666420/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..-nfZk6vneRueL7x2gvhaTQ.DCk0SonxzFc_r5z4QAPJrjRqu-d_6KgEKOvKmlf4z1zlqQBrZ2qsd1T-r3L_djSWn-W58trDbpNTHFuf8tKiL7Akq-vZwKMkLXv4_1dqiMCIUpa7lhdXW_Ss25eREE8U.HG-fudsk_AA4Iefzv5-n5A/__results__.html#Wordclouds---Frequent-words:)上找到它们。)

*Rhodium* 构建了一个字符长度直方图以及类别之间的热图，发现一些标签高度相关；例如，侮辱有 74%可能也是淫秽的。

*Jagan* 绘制了一些单词云、热图和交叉表，观察到:

> 一个严重的有毒评论总是有毒的
> 除了少数例外，其他类别似乎是有毒的子集

## 特征工程

*铑*小写文本，手动把缩写变成东西，手动清理标点符号。

*Jagan* 绘制各种特性与毒性的关系图，寻找相关性。发现之一是:垃圾邮件发送者往往更具毒性。

![](img/36f30f534fcccdb34deb7bd31ea006a1.png)

Jagan discussing feature engineering

对于单个单词和成对单词， *Jagan* 和 *Rhodium* 都使用 TF-IDF 绘制顶部单词，描述如下:

> TF 代表词频；本质上，一个单词在文本中出现的频率…你可以把它理解为相对文本频率与整体文档频率的归一化。这将导致特定作者特有的单词脱颖而出，这也是我们为了建立预测模型而想要实现的。— [正面还是反面](https://www.kaggle.com/headsortails/treemap-house-of-horror-spooky-eda-lda-features)

## 外卖食品

似乎所有作者都遵循一些最佳实践，包括小写文本、处理缩写和清理标点符号等都是作者关注的领域。然而，一些作者也认为这些可能是潜在的特征，而不仅仅是噪音(例如，Francesco 发现了打字错误和毒性之间的相关性)。

## [阴森森的作者识别](https://www.kaggle.com/c/spooky-author-identification)

![](img/11a731c0077608fb179226b9580120d6.png)

by [Gael Varoquaux](https://www.flickr.com/photos/gaelvaroquaux/29632530995/in/photolist-M9wt5P-97P7tg-4vzLRF-61r11U-Zt2GHV-cY8aNJ-cY7ZgL-UXxYV9-b4qibP-4tm3wK-7haukg-2JiX6D-cVsp9-cY7XLU-4eeRFT-8PsYcb-cY7X8j-5jUhKv-jVRzRb-97Sb5A-7aBbJH-dZNRw2-smkRf-gxqQt3-aqqb74-gxs9eF-62dAE-FnZJs-62dXh-ZWp8CL-DpiJqc-WuwzSK-FnXvG-Ef1yLk-7omXUv-r5iPPD-pDGN7f-61hnvE-FnZKU-FnXv1-n28gM8-quLHEs-iAsBz-WBEwee-5z3uaW-pEQPCo-efPVZU-YbEZgy-dVfyAo-nHKteU)

[幽灵作者识别](https://www.kaggle.com/c/spooky-author-identification)提供了三位恐怖主题作者的文本片段——埃德加·爱伦·坡、惠普·洛夫克拉夫特或玛莉·渥斯顿克雷福特·雪莱——并要求参与者建立一个模型，能够预测哪位作家创作了特定的一段文本。

我选择进行分析的 EDA 是由*提供的[怪异 NLP 和主题建模教程](https://www.kaggle.com/arthurtok/spooky-nlp-and-topic-modelling-tutorial)各向异性*，[教程详细怪异趣味 EDA 和建模](https://www.kaggle.com/ambarish/tutorial-detailed-spooky-fun-eda-and-modelling)由 *Bukun* 提供，以及由*头或尾*提供的 [Treemap House of Horror 怪异 EDA LDA Features](https://www.kaggle.com/headsortails/treemap-house-of-horror-spooky-eda-lda-features) 。

这个数据集的有趣之处在于它的简单性；除了作者之外，文本附带的非结构化数据非常少。因此，所有的数据库都只关注不同的语言解析和分析方法。

每个作者首先检查数据集，挑选几行，并绘制每个作者的故事数量。 *Bukun* 还会查看每个作者的字数，而*各向异性*会绘制一个总字数的条形图:

![](img/b0c32d4f362f0166afe4feb4791b4bd9.png)

> 注意到这个词频图中出现的单词有什么奇怪的地方吗？这些话实际上告诉了我们玛丽·雪莱在她的故事中想要向读者描绘的主题和概念吗？这些词都是非常常见的词，你可以在任何其他地方找到。不仅在我们三位作者的恐怖故事和小说中，而且在报纸、儿童读物、宗教文本中——实际上几乎所有其他的英语文本中。因此，我们必须找到一些方法来预处理我们的数据集，首先去除所有这些经常出现的单词，这些单词不会给表格带来太多。—各向异性

每位作者都构建了词云，最大程度地显示了最常用的词:

![](img/76ea2c309da535153a2c9a6a6c216c35.png)

Heads or Tails builds a word cloud of the 50 most common words

*Heads or Tails* 还绘制出每个作者的整体句子、句子和单词长度，并发现作者之间细微但可测量的差异。

*各向异性*和*卜坤*讨论标记化，去除停用词:

> 这一阶段的工作试图将相似单词的许多不同变体缩减为单个术语(不同的分支都缩减为单个词干)。因此，如果我们有“运行”、“运行”和“运行”，你真的会希望这三个不同的单词合并成一个单词“运行”。(当然，你失去了过去、现在或将来时态的粒度)。—各向异性

在标记化、停用词移除和词条化之后，*各向异性*重建前 50 个词的图:

![](img/701682b40e1f21943437086ebdbc53d5.png)

*Bukun* 将他最喜欢的 10 个词按照作者进行分类，找到了不同的组合:

![](img/ac0b8c73745068f997aad0d9906b3e81.png)

*Heads or Tails* 也是这样做的，在标记化和词干化之后，另外查看作者的热门词。

*Bukun* 和 *Heads or Tails* 都使用 TF-IDF 来为特定作者找到最“重要”的词。

![](img/e16e502e29a459753cf4e38ce577cf82.png)

Heads or Tails plots the most significant words by author in a bit of a different chart

*Bukun* 查看顶级二元模型和三元模型(分别是两个和三个单词的集合)。

![](img/fc6257b732654017904a3ae5192bacc1.png)

Heads or Tails plots the word relationships for bigrams

*Bukun* 和*正面或反面*都执行情感分析，并查看每个作者的总体负面评价。

*Bukun* 使用一种叫做“NRC 情绪词典”的东西来检查每个文本片段中“恐惧”、“惊喜”和“喜悦”的数量，并使用单词云、表格、条形图来可视化各个作者的情绪。

![](img/7e67bf6c89eca3271887de038c6b42ac.png)

Bukun plots a word cloud for words matching Joy

## 特征工程

Bukun 建议添加一些可能的特性，包括逗号、分号、冒号、空格、带大写字母的单词或以大写字母开头的单词，以及每一个的图表。对于一些作者来说，这些特征之间确实存在某种关联。

*正面或反面*注意到:

> 我们已经注意到，我们的三个作者可以通过他们最突出的人物的名字来识别；玛丽·雪莱写的是“雷蒙德”，洛夫克拉夫特写的是“赫伯特·韦斯特”。但是一般的名字呢？是不是有些作者在某些情况下更倾向于用名字？在句子或字符长度之后，这是我们寻求知识的第一个特征工程概念

从这个角度来看，*正面或反面*依赖于`babynames`包，该包提供了给定年份最受欢迎名字的列表，为数据增加了一个额外的特性。

*Bukun* 和 *Heads or Tails* 都查看作者之间的性别代词细分，而 *Heads or Tails* 还查看句子主题、每个作者的起始单词和最后一个单词、独特单词的数量、每个句子中独特单词的比例、对话标记和头韵(这是一个很酷的想法！)

![](img/b7af9e6486f9d0195746cf37efbb9a92.png)

heads or tails plots various measurements of alliteration by author

*正面还是反面*以展示功能交互的冲积图结束他的内核:

![](img/7c19e607c5008e626a345fddbd7b968c.png)

Heads or Tails’ alluvial plot showcasing feature interaction

## 外卖食品

这是一个值得研究的有趣竞争，因为文本片段更长，并且没有结构化数据可以依赖。

内核倾向于利用 NLP 最佳实践，比如小写单词、词干和标记化。内核也倾向于使用比有毒内核更先进的技术，如情感分析和二元三元模型分析。

两次比赛，内核作者都用了 [TF-IDF](https://www.kaggle.com/headsortails/treemap-house-of-horror-spooky-eda-lda-features) 。

对于功能工程，作者设计了各种新功能，包括每句话的平均字数、标点符号的选择以及单词是否重复。

# 形象

到目前为止，数据集都是纯粹基于文本的(语言、字符串或数字)。我选择查看的最后两个数据集是基于图像的。

我研究的两个竞赛([肺癌](https://www.kaggle.com/c/data-science-bowl-2017/)和[树叶分类](https://www.kaggle.com/c/leaf-classification/))都比我研究的其他竞赛更具领域特异性。因此，这些分析倾向于假设一个先进的观众，作者跳过了初步的分析，有利于探索不同的图像分析技术。

我在所使用的可视化技术方面看到了很大的多样性，以及工程化的特性。特别是，肺癌竞赛中的一些作者利用了现有的医学知识，以便设计出极具领域特异性的特征。我不能说这些功能有多有效，但我可以说它们产生的视觉效果令人惊叹。

## [树叶分类](https://www.kaggle.com/c/leaf-classification/)

树叶分类比赛包括 1，584 张树叶的蒙版图片，按物种组织。参与者被要求建立一个模型，这个模型能够将新的图片分类到其中一个类别。

我选择用于分析的 EDA 是由 *lorinc* 的[图像特征提取](https://www.kaggle.com/lorinc/feature-extraction-from-images)，由 *selfishgene* 的[用叶子数据集可视化 PCA](https://www.kaggle.com/selfishgene/visualizing-pca-with-leaf-dataset)，以及由 *Jose Alberto* 的[快速图像探索](https://www.kaggle.com/josealberto/fast-image-exploration)。

一个好的第一步是看树叶的图像，这是两个 EDA 的开始。

![](img/7c630184f6ac29f43f96c26ace26885e.png)

selfishgene examines the leaf specimens

何塞绘制了各种各样的物种，并指出每个物种有 10 张图片。他还研究了一个类别内的树叶之间的相似性:

![](img/e7f34c73fe4befa738efc577ed6faa53.png)

Jose compares leaves within a category

与此同时， *lorinc* 直接进入分析，定位每片叶子的中心并应用边缘检测。lorinc 还将叶子的轮廓转换成极坐标，以便更有效地测量叶子的中心:

> 稍后，当我们从形状生成时间序列时，我们可能希望切换到另一种中心性度量，基于该中心的效率，使用边缘和中心之间的距离。一种方法是测量中心和边缘之间的(欧几里德)距离……但是有一种更好的方法——我们将笛卡尔坐标投影到极坐标中。

*selfishgene* 选择查看图像的变化方向，写道:

> 每个图像可以被认为是高维图像空间中的不同“方向”

![](img/2cae8c00e48dafcdcf860cb57300be25.png)

selfishgene looks at the variance of a leaf image

*selfishgene* 也花了一些时间研究图像重建、平均图像周围的模型变化和特征向量；他解释道:

> 最上面一行包含每个特征向量的数据分布(即沿该“方向”的直方图)，第二行包含我们在前面的图中已经看到的内容，我们称之为方差方向。第四行包含叶子的中间图像。请注意，这一行对于所有特征向量都是相同的。第三行保存每个特征向量的第 2 个百分位数的图像。更容易认为这是中值图像减去特征向量图像乘以某个常数。

![](img/af7d697f622f9faba80a1e95f9ffeca9.png)

selfishgene looks at model variations

## 特征检测

*lorinc* 建议将每个样本一分为二，作为两个样本对待(尽管他并不追求这种方法)。 *lorinc* 从时间序列中寻找局部最大值和最小值(例如，在极坐标中绘制的叶子)并记录:

> 好吧，我自己也吃惊。这一点做得很好。我想，我可以由此构建一个极其高效的特性。但是这种方法还不够健壮。
> 
> 不是找到尖端，而是找到离中心距离最大的点。(请看第 19 页)
> 
> 在更复杂或不幸旋转的叶片上，它将悲惨地失败。(看第 78 页)

![](img/46fd8432c0c3b329e30d5413fd613018.png)

lorinc measures the minima and maxima of a leaf plotted in polar coordinates

在发现每片叶子周围存在噪音之前，lorinc 从那里开始讲述数学形态学。他花了一些时间想出如何从图像中去除噪声，并以一幅可爱的图像结束，该图像显示了叠加在叶子上的距离图:

![](img/1097caa522a3230271122fea94d894fd.png)

lorinc measures the distance from the center of a leaf

## [肺癌](https://www.kaggle.com/c/data-science-bowl-2017/)

我选择分析的 EDAs 分别是[Guido Zuidhof*的*](https://www.kaggle.com/gzuidhof/full-preprocessing-tutorial)全预处理教程，Mikel Bober-Irizar*的[探索性数据分析](https://www.kaggle.com/anokas/exploratory-data-analysis-4)和 *Alexandru Papiu* 的[探索性分析可视化](https://www.kaggle.com/apapiu/exploratory-analysis-visualization)。*

![](img/598dd546cf0aed04e477f31ebfc05111.png)

anokas examines the metadata for a single image. You can see that patient date has been rendered anonymous (1/1/1900)

我看的最后一个图像竞赛是 [2017 数据科学碗](https://www.kaggle.com/c/data-science-bowl-2017/)，它要求参与者检查一系列图像，并预测患者是否患有癌症。虽然这场比赛的特点是结构化数据(嵌入图像本身的元信息)，但其中一些数据是匿名的，这意味着原本具有预测价值的特征(如患者的年龄)被删除了。这意味着所有的内核都专注于图像分析。

在三个核心作者中， *Guido* 是唯一一个讨论他的医学图像工作背景的人，在他对数据集的特定领域分析中显示:

> Dicom 是医学成像领域事实上的文件标准。…这些文件包含大量元数据(例如像素大小，即一个像素在现实世界中的每个维度上有多长)。扫描的这种像素大小/粗糙度因扫描而异(例如，切片之间的距离可能不同)，这可能损害 CNN 方法的性能。我们可以通过同构重采样来解决这个问题

其他两位作者从数据集和图像本身的更一般的探索开始他们的 EDA。

*apapie* 从检查图像的形状开始，而 *anokas* 从查看每个患者的扫描次数、扫描总数和每个患者的 DICOM 文件直方图开始，同时进行快速的完整性检查，以查看行 ID 和患者是否患有癌症之间是否有任何关系(没有发现任何关系，这意味着数据集已经很好地排序)。

*Alexandru* 获取像素分布并绘制它们:

![](img/ec2e97cc2f4f77f7c0896f5f5074271b.png)

> 有趣的是，该分布似乎大致呈双峰分布，一组像素设置为-2000，可能是因为缺少值。

*Guido* 在他的 EDA 中更清楚地解释了这是为什么，即由于 HU 单位所代表的(空气、组织和骨骼):

![](img/2f672a33a2af1e58d9474a267b417e27.png)

## 形象

每个作者继续检查图像本身:

![](img/c2ea0b76590b329fc813baa825aa58e9.png)

anokas looks at a set of patient images side by side

*Alexandru* 从 X 角度查看图像

![](img/46c393011dcc01a218b90cf491f6890a.png)

Alexandru looks at images from the X angle

![](img/1fee1c31d7c5be164528cc86be23bfac.png)

anokas builds a gif that moves through a set of patient images

Alexandru 花了一些时间探索边缘检测是否可以增强图像。

![](img/1e1f9f8f0168de55f60bc2d205ae6fbc.png)

After increasing the threshold, Alexandru was able to render some visually striking images

亚历山德鲁的结论是:

> 有趣的结果，然而这里的问题是过滤器也将检测肺部的血管。因此，区分球体和管道的某种三维表面检测更适合这种情况。

同时， *Guido* 讨论了重采样，重点是 DICOM 图像的基本特性:

> 扫描可以具有[2.5，0.5，0.5]的像素间距，这意味着切片之间的距离是 2.5 毫米。对于不同的扫描，这可能是[1.5，0.725，0.725]，这对于自动分析(例如使用 ConvNets)可能是有问题的！处理这种情况的一种常见方法是将整个数据集重采样到某个各向同性分辨率。如果我们选择将所有内容重新采样为 1mm1mm1mm 像素，我们可以使用 3D convnets，而不必担心学习缩放/切片厚度不变性。

后来在他的 EDA 中， *Guido* 能够通过组合多个 DICOM 图像来绘制内腔的 3D 图:

![](img/31c6cdcd987f5c9f076bbf0f115d1386.png)

而另一个版本，在去除了周围的空气以减少内存之后:

![](img/0ed1bd1201f391b2d06748300750bcdf.png)

## 外卖食品

这场比赛是我见过的内核差异最大的比赛。 *Guido* ，鉴于他对医学图像格式的熟悉，能够利用这一背景得出更加微妙的结论。也就是说，其他两位作者缺乏医学知识并不妨碍他们得出同样有趣的结论。

# 结论

事实证明，对于不同类型的数据，有一些强有力的模式可以指导方法。

对于**结构化数据**竞赛，数据分析倾向于寻找目标变量和其他列之间的相关性，并花费大量时间可视化相关性或对相关性进行排名。对于较小的数据集，您只能检查这么多列；在[大竞争](https://www.kaggle.com/c/titanic)中的分析在检查哪些列和以什么样的顺序方面趋于一致。然而，不同的编码人员使用了非常不同的可视化方法，似乎在选择设计哪些特性方面有更多的创造性。

**自然语言**数据集在作者如何处理和操作文本方面与 EDA 有相似之处，但作者选择设计的特征有更多的可变性，以及从这些分析中得出的不同结论。

最后， **Image** 竞赛在分析和特征工程方面表现出最大的多样性。我看到的图像比赛大多针对高级观众，并且在相当特定的领域，这可能导致了更高级的多样性。

随着数据集变得更加专业化或深奥，介绍性分析和解释的数量减少，而深度或专业化分析的数量增加，这是有道理的，事实上这就是我所看到的。虽然不同类型的数据有明显的趋势，但领域知识起着重要的作用。在肺癌和 leaf 竞赛中，利用领域知识进行了更深入的分析。(说来有趣，我在自己的研究中见过这种情况；杰瑞米·霍华德在他的 [fast.ai](https://fast.ai) 课程中，讨论了罗斯曼数据集，以及最成功的模型如何整合第三方数据集，如温度、商店位置等，以做出更准确的销售预测。)

对于作者何时处理特征工程，没有一致的过程，一些人选择在他们开始分析时就开始，而另一些人在他们的初始分析完成后保持一个离散的步骤。

最后，我看到的每一个笔记本都有明确的读者群(初学者或高级)，这影响了分析和写作。更受欢迎的比赛，或者那些针对更普通观众的比赛，有详尽的分析数据。在这些电子数据分析中，我也看到了一种趋势，即在分析的同时穿插补充性的文章或使用叙事手段，作为帮助初学者更好地理解技巧的工具。相比之下，面向领域专家的笔记本倾向于去掉多余的框架，许多还跳过了基本的数据分析，而是直接进入特定领域的技术。

*特别感谢* [*米歇尔·卢*](http://michellelew.com/) *，* [*阿里·齐尔尼克*](http://ari.zilnik.com/) *，* [*肖恩·马修斯*](http://seanmatthe.ws/) *，以及* [*贝瑟尼·巴西尔*](http://visiongrowth.org) *为本文审稿。*

*原载于*[*thekevinscott.com*](https://thekevinscott.com/common-patterns-for-analyzing-data)