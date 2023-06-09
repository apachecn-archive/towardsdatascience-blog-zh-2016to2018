# 数据科学过程

> 原文：<https://towardsdatascience.com/the-data-science-process-a09c5bc0cc4?source=collection_archive---------11----------------------->

对于我最近在大会数据科学沉浸式课程中的项目，我遇到了相当多的障碍。虽然我在过去的四周里已经讨论了大量的材料，并为我的敏锐度增加了不少技能，但爱荷华州的白酒销售项目向我揭示了我对数据科学以及进行彻底分析的相关最佳实践有太多的不了解。我很乐观，但有很多事情我希望我能以不同的方式去做。

我发现这个领域最具挑战性的事情是阅读和解释文档。从熊猫，到 Numpy，到 scikit-learn，到 Seaborn，尽管导师提供了看似简单的例子，但事情并不容易。这门课程是为我们设计的，让我们超越讲座中所涵盖的内容，这也是我意识到自己最大的困难所在。这需要时间。人们很容易迷失在几个小时的 YouTube 教学视频和由经验丰富的程序员为经验丰富的程序员编写的神秘格式中。面对如此丰富的资源，寻找解决方案可能会很困难，每一个小小的成功都会遇到至少两个障碍。

这篇文章不是发泄，而是要具体展示什么有效。希望我能够利用一些辛苦学到的洞察力来简化未来的事情。

**EDA 和清洗**

导入 csv 时，将列名改为小写，并在出现空格的地方插入下划线。

dataframe_cols = ['col_1 '，' col_n']

我们需要使用 dataframe 函数对日期进行转换，使其成为 python 易于阅读的格式。

data frame[" date "]= PD . to _ datetime(data frame[" date "])

**哪里出了问题**

*缺失值和数据类型至关重要*。我天真地认为我不应该担心那些不影响我的变量的列。

此外，许多数据确实需要修改。字符串需要转换成浮点数。货币值需要去掉美元符号和逗号。不早点这么做最终会浪费时间，让我感到沮丧。

data frame . sales = data frame . state . sales . str . replace(' $ '，' ')

data frame . sales = data frame . sales . str . replace('，'，' ')

剩下的 EDA 步骤进展顺利，但是我仍然对最佳实践有疑问。例如，在不同的列中有相当多的重复项，而我没有按县划分销售额这一事实将需要相当多的额外步骤，例如创建虚拟变量和考虑人为错误。

我遇到的另一个问题是自我诱导的。出于某种原因，我认为这项任务要求我们包含多个独立变量，所以我查看了各种因素，如瓶容量、州瓶成本、州瓶零售等与销售相关的因素。这不仅是错误的，整个要点是使用 2015 年 Q1 销售额和 2015 年剩余 9 个月之间的线性回归进行交叉验证，以创建一个可以帮助我们预测 2016 年最后 9 个月的模型。尽管有这些缺点，我还是学会了如何利用一个特定的函数来查看独立变量之间的相关系数(皮尔逊系数)。虽然它不适用于这个特定的作业，但我知道它在将来会有用，我们在课堂上也讨论过它的一般概念。

dataframe.corr(method='pearson '，min_periods=1)

总的来说，这项作业似乎是为了让学生熟悉 groupby 函数而设计的。因为我想按商店查看销售额，所以我使用了下面的代码并创建了一个新的数据框。

stores _ sales = dict(data frame . group by([' store _ number ']). sales . agg(sum))

因为有两种不同用途的数据，所以我在 pandas 中使用布尔方法来创建新的数据帧。

year 2015 = data frame[data frame . date< ‘2016–01–01’]
year 2016 = data frame[data frame . date>= ' 2016–01–01 ']

然后，我使用 more dataframe 函数按季度对酒类销售进行排序，这将创建一个单独的列。

dataframe['季度']=dataframe['日期'].dt.quarter

q1 =数据帧。quarter == 1

sales _ per _ store _ Q1 _ 15 = year 2015[Q1]。group by([' store _ number ']). sales . agg(sum)

sales _ per _ store _ r _ 15 = year 2015[reminder 15]。group by([' store _ number ']). sales . agg(sum)

虽然事情似乎进展顺利，但我的关键错误(以及其他一些错误)是没有考虑到开店数量的变化。通过使用 sales_per_store_q1_15.shape 和 sales_per_store_r_15.shape，我了解到我无法创建模型。意识到这一点后，我非常心烦意乱，尤其是当时间是至关重要的时候。

这个项目不仅是时间管理上的一堂艰难的课，它还留下了几个没有答案的问题。出于这个原因，这将不会是最后一次与爱荷华州的酒数据集会合。敬请关注稍后发布的更新。