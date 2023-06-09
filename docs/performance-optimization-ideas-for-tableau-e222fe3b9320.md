# Tableau 的性能优化思想

> 原文：<https://towardsdatascience.com/performance-optimization-ideas-for-tableau-e222fe3b9320?source=collection_archive---------13----------------------->

![](img/1d9a5b22897729a4fceed7e0af469678.png)

数据无处不在，它本身正在成为一种货币。像脸书这样的公司将信息作为他们的主要收入来源。为了有用，数据需要被处理、理解，甚至转换成可爱的图形表示。Tableau 可以成功地做到所有这些，并且让用户继续在本地系统中工作，如电子表格、关系数据库、云环境或 OLAP。通过一个简单的连接，所有这些都成功地导入到 Tableau 中，并准备接受分析。然而，当出现明显的延迟和明显的性能下降时，您能做些什么呢？

# 这是谁的错？

每次发现性能下降时，您都需要确定原因。是硬件还是软件？是本地机器造成的还是服务器造成的？你能实施快速解决方案吗，或者你需要重新评估你的工作模式吗？

# 过时的硬件

要解决的最直接的问题，尽管不是最便宜的，是升级本地设备。要了解这是否有必要，请在您怀疑速度太慢的计算机和一台好得多的计算机上测试同一工作簿。如果有显著差异，请升级。

# 服务器问题

如果工作簿位于服务器上的共享数据连接上，可能是您过度使用了可用资源。例如，如果计算是在共享源中定义的，您可能希望使用本地源进行故障排除，以避免服务器过载。

# 直播的麻烦

想想保持 Tableau 直播的必要性。除非项目必须有实时提要，否则通过创建定期更新的摘录来节省资源。

当实时流是一个基本条件时，考虑定制 SQL 的必要性。这些是一些最低效的连接，应该尽可能地加以限制。为了提高速度，直接在 Tableau 中定义连接，而不是 SQL。看看那些需要加倍努力的不必要的条款。这样的例子是“ORDER BY ”,因为 Tableau 在加载后会对数据进行重新排序。

# 更好的数据管理

数据对性能有直接影响。始终只处理各自任务所需的数据。空闲列只会降低 Tableau 环境的速度。只提取一个样本或完全删除不必要的列。这将转化为更短的刷新时间和更高的速度。

摘录是你最好的朋友。把它们想象成一个“手提箱”,你把当前任务需要的数据放在里面，就像你度假时只带你需要的东西，而不是家里的所有东西。甚至有一个案例研究描述了使用这种方法后，报告的计算时间减少了 99%。

# 过滤微调

快速滤镜是你的画面表现的无声杀手之一。这些缺省值看似无害，但实际上，对于仪表板中出现的每个缺省值，都有一个在后台执行的连接查询。当然，保留那些你需要的，但是也考虑用“动作”过滤器替换，因为这些过滤器不会触发查询。

减少不必要的服务器资源负担的另一种方法是在通过上下文过滤器需要连接之前计算连接。这是一种创建非规范化表的方法，速度可节省 90%。事实上，这可以作为良好的实践。

# 关于计算的决定

逻辑条件会对分配的资源造成真正的损失。一些最贪婪的子句是 IF-ELSE 结构。如果不是太多，只要有与值的比较，这些都可以被布尔条件成功替代。

数据的类型对计算速度有很大的影响。要知道字符串是最容易使用的资源，其次是日期、布尔值，最后是数字。

另一个技巧是去掉使用组，用“格”来代替。当添加满足底层条件的新成员时，这甚至更有用。在分组的情况下，这应该是手工完成的，因此对于输入来说也是节省时间的操作。

如果您在本地进行计算，这会降低工作簿的速度。尽量利用服务器方法的优势。此外，无论如何都要避免在行级别使用参数进行计算。

# 标志和图像

每个数据点被称为一个标记，显示它会降低系统速度。想想每一列或每一行的必要性，不要因为你太懒就把它们摆在那里。

将图片的使用限制在绝对必要的范围内。尝试使用透明背景的 png，既能达到设计目的，又能占用更少的空间。

# 布局提示和技巧

每个布局都需要自己的资源，超过四个会大大降低仪表板的性能。尽量在你的小组中包含练习册，并确保你最大限度地使用你选择的练习册。

这听起来可能令人惊讶，但是为你的仪表板设置一个尺寸可以提高性能。原因在于，将它设为“自动”，这是默认设置，将迫使工作簿根据每个不同用户的屏幕大小来适应他们的偏好。对于环境来说，这类似于为每个用户打开不同的仪表板，即使信息是相同的。

# 优化 Tableau 有意义吗？

Tableau 是 BI 最强大的工具之一。这是因为它主要是一个具有计算能力的数据可视化工具，对技术技能的要求很低，而且非常直观。它还可以处理大量数据，同时连接到实时源或与其他电子表格环境通信。

由于这种多功能性，使用这个工具并使其尽可能快速高效是有意义的。当然，它并不完美，但通过首先解决硬件问题，然后更加关注数据管理和计算逻辑，只需稍加调整，它就可以变得快如闪电。