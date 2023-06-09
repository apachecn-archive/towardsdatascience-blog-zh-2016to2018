# 作为一名数据人员，我学到了 8 件事

> 原文：<https://towardsdatascience.com/8-things-ive-learnt-being-a-data-guy-e3b99b1acf22?source=collection_archive---------4----------------------->

![](img/49b761f5c4ff61967f68f32b1f8a235e.png)

Lexer Sydney Office

在上周的一次 Python 见面会上，我最害怕的问题出现了:“那么你是做什么的？”恐惧的感觉来自于不得不解释我是如何负责三个不同职位的焦虑。那我该说什么？

我是一名数据开发人员、数据科学家和数据工程师。相当多，特别是当我说我也是一名火箭工程师的时候。

今天是我在 Lexer 工作的第 268 天，这是一段怎样的旅程！当我提炼出一些我的技术和商业知识时，这篇文章旨在给局外人一个窥探创业公司迷人世界的机会。

# 技术的

# 1.正确命名您的变量！

作为一名航空航天工程背景的人，编码只是达到目的的一种手段，我对良好的编码实践一无所知。当我开始用 Ruby 编写脚本时，我在 Lexer 的导师很快指出像`sum_array`或`final_hash`这样的变量名是没有意义和多余的。

> 相反，命名变量是为了描述它们的功能，而不是它们的数据类型。

假设我想使用一个假设的 count 函数来计算`["apple","orange","banana","apple"]`中`"apple"`的出现次数，这个函数接受一个字符串数组和要计算的搜索字符串。有利的语法应该是`n_apples = count(fruits, "apple")`而不是`count_val = count(fruits, "apple")`

# 2.少相信你的眼睛，多相信你的代码。

假设你有一个柠檬水摊位，你想分析你的销售业绩。你让你的助手 Roger 在 excel 电子表格中记录所有交易，分为三列`Name`、`Total Spent`、&、`Date of Lemonade purchase`。

作为一名数据工作者，你自然不相信人类能够生成干净的数据集，所以你决定在分析 Roger 的电子表格之前对其进行感官检查。

前几行看起来都很好，名字以正确的格式输入。总数和日期是合理的。问题是电子表格包含 1000 个事务。您可以继续目测数据，一次一行，但这将花费很长时间，而且无法保证您的眼睛会错过数据格式或总花费值中的细微错误。

更聪明的选择是查看数据的基数。像`cut -d '|' -f 2 lemonade_purchase.csv | sort | uniq -c | sort -rn`这样的 bash 命令将汇总所有总花费值，并根据出现次数对它们进行排序:

```
800 2.5
100 5
50  10
50  $ 
```

就像这样，您可以看到其中 50 笔交易的交易金额为`$`，这毫无意义。现在，您将研究这个问题的可能解决方案，并继续清理数据。

# 3.测试、测试和更多测试

在加入 Lexer 之前，这是我写代码的过程:`Write Code --> Count my blessings --> Execute --> Check if output looks right`。这是一个直觉游戏。

在 Lexer，我被引入了测试驱动开发(TDD)的美丽世界。测试指定您正在编写的特定代码段的输入和期望输出，然后它检查您的代码的实际输出是否与期望输出相等。

测试应该尽可能的具体和多样。测试给你信心，你的代码正在按预期工作。它用可靠的工作证据取代了直觉。

# 4.边缘情况下的设计

当我第一次开始数据争论时，我会很快形成一个清理数据集的攻击计划，并天真地期望它能完美地工作。我几乎不知道，当您有一个数百万行和 40-100 列的数据集时，您肯定会遇到您最初的攻击计划没有考虑到的边缘情况。这造成了严重的延误和方法的重复。

> 总是假设数据质量很差，所以你可以设计你的争论方法在最坏的情况下工作。

# 5.制作可伸缩代码

当你的 Ruby 脚本花了一个小时从 200 万行文本中解析并提取相关信息后，代码效率就跃升到了你的首要任务。在 Lexer，我学会了从大处着眼，总是问自己如何将一个解决方案大规模应用到几十亿字节的文本数据中。俗话说时间就是金钱，你通过代码效率节省的每一秒都是有价值的。

# 商业

# 6.想想你的客户如何使用你的产品

在 Lexer，我们帮助公司将数据用于真正理解和吸引客户。由于我的大部分工作都围绕着 Lexer 平台的技术工作，因此很容易脱离客户需求，转而沉迷于构建“酷”的功能，这些功能使用起来很酷，看起来很酷，但可能不那么有用。

# 7.只向需要您提供的解决方案的人销售

我在 Lexer 的第一个月，我让我们的一位业务开发经理卖给我一支笔。他说的第一句话是“你需要这支笔吗？”。我说‘不’。他说‘好吧。那就没必要把笔卖给你了。到目前为止，对我来说，销售意味着无论如何都要说服你的潜在客户购买你的产品。理论上，只要有足够的时间和努力，这是可行的，尽管成功率较低。或者，您可以尝试寻找那些拥有由您的产品实现的用例的客户。虽然你需要做额外的工作来发现这些潜力，但与“喷洒和祈祷”方法相比，这大大提高了你结束的机会。

# 8.找到需要回答的问题

这项工作最难的部分不是找到要回答的问题。这些为解决方案提供了背景，为我们提供了可操作的见解。许多组织都非常清楚“大数据”能为他们带来什么。例如，客户参与度的提高、收入的增加、流失率的降低等。然而，为了得到这些结果，大多数组织会被如何处理他们的数据所困扰。在这种情况下，问“如何？”是拼图中重要的一块。你如何利用这些数据为自己谋利？