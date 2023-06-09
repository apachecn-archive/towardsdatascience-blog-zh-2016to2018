# 张量流文件系统—以不同方式访问张量

> 原文：<https://towardsdatascience.com/tensorflow-filesystem-access-tensors-differently-888bce1d68e7?source=collection_archive---------16----------------------->

![](img/c14fe8f80acadd34724c6a3a8a30a2e9.png)

Tensorflow 很棒。真的，我是认真的。问题是它在某种程度上是伟大的。有时候你想做非常简单的事情，但是 tensorflow 却在为难你。我写 [TFFS](https://github.com/yoel-zeldes/tffs) (TensorFlow 文件系统)背后的动机可以被任何使用过 TensorFlow 的人分享，包括你。

我只想知道一个特定张量的名字是什么；或者它的输入张量是什么(忽略运算)。

使用 tensorboard 可以轻松回答所有这些问题。
当然，你只需打开图形选项卡，并目视检查图形。真的很方便吧？如果你想对图表有一个总体的了解。但是如果你很专注，并且有一个特定的问题想要回答，使用键盘是一个不错的选择。

**那么为什么不在 python shell 中加载图形并检查它呢？** 这是可行的，但是每次我想做那个任务的时候都要写这几行代码？必须记住如何加载图形，如何寻找张量，如何获得它的输入…当然，这只是几行代码，但一旦你一次又一次地重复同样的任务，就该写脚本了！

那么为什么不写一个交互式脚本呢？你是指一个脚本，它给出了模型的路径，为你加载它，并提供实用函数来减轻你写张量流代码的痛苦？好吧，我们可以这么做，但那不会比我要给你看的更棒！

声明:如果你想要一个有意义的解决方案，停止阅读这里，只使用交互式脚本方法。只有当你想学习一些不同的东西时，才继续阅读；)

# 文件系统拯救世界！

张量的名称有斜杠——与 UNIX 文件系统非常相似。想象一个有张量流文件系统的世界，其中目录类似于张量流范围，文件类似于张量。给定这样一个文件系统，我们可以使用传统的 bash 来做我们想做的事情。例如，我们可以通过运行`find ~/tf`列出所有可用的作用域和张量——假设`~/tf`是 tensorflow 文件系统的挂载位置。想只列出张量？没问题，用`find ~/tf -type f`就行了。

嘿，我们有文件，对吧？它们的内容应该是什么？让我们运行`cat ~/tf/.../tensor_name`。哇！我们得到了张量的值——很好……这只有在张量不依赖占位符的情况下才有效，原因很明显。

如何得到张量的输入呢？嗯，你可以跑`~/tf/bin/inputs -d 3 ~/tf/.../tensor_name`。这个特殊的脚本将打印递归深度为 3 的输入的树形视图。不错…

![](img/58a18b185827e6e303f575bfaeb6a0d3.png)

好吧，我加入。我们如何实现它？这个问题问得好。我们可以在用户空间(FUSE)中使用文件系统。这是一种允许我们在用户空间实现文件系统的技术。它为我们省去了进入低层次领域的麻烦，如果你以前没有做过，这真的很难做到(并且实现起来很慢)。包括用 C 写代码——恐怖！我们将使用名为 [fusepy](https://github.com/fusepy/fusepy) 的 python 绑定。

在这篇文章中，我将只解释实现中有趣的部分。完整的代码可以在这里找到。包括文档在内，只有 345 行代码。

首先我们需要加载一个张量流模型:

1.  使用`tf.train.import_meta_graph`导入图形结构。
2.  如果模型经过训练，使用`saver.restore`加载重量。

# 将张量映射到文件

接下来，我将描述主类。构造函数中有几件有趣的事情。首先，我们称之为`_load_model`。然后，我们将图中的每个张量映射到文件系统中的一个路径。假设一个张量的名字是`a/b/c:0`——它将被映射到路径`~/tf/a/b/c:0`，假设挂载点是`~/tf`。

每个目录和文件都是使用`_create_dir`和`_create_tensor_file`函数创建的。这些函数返回一个简单的 python 字典，其中包含关于目录或文件的元数据。

我们也叫`_populate_bin`，后面我会讲到。

# 使用 fusepy

fusepy 要求你实现一个扩展`fuse.Operations`的类。这个类实现文件系统支持的操作。在我们的例子中，我们想要支持读取文件，所以我们将实现`read`函数。当被调用时，这个函数将计算与给定路径相关的张量。

担心`printoptions`部分？当实现文件系统时，你需要知道文件的大小。为了知道大小，我们可以评估所有的张量，但是这需要时间和内存。相反，我们可以检查每个张量的形状。给定它的形状，并且给定我们使用一个格式化程序在结果中输出每个条目的固定数量的字符(这就是`_fixed_val_length`出现的地方)，我们可以计算大小。

# 获取输入和输出

虽然张量流观测仪的结构类似于文件系统，但张量输入和输出却不同。因此，我们可以不使用文件系统来获取输入和输出，而是编写一个可以如下执行的脚本:

`~/tf/bin/outputs — depth 3 ~/tf/a:0`

结果将如下所示:

```
~/tf/a:0
├── ~/tf/b:0
└── ~/tf/c:0
    └── ~/tf/d:0
    |   └── ~/tf/e:0
    └── ~/tf/f:0
```

不错！我们有输出树！要实现它，我们要做的就是:

1.  获取数据，这是从每个张量到其输出的映射。
2.  实现一个输出树的递归函数。这并不复杂(它花了我 6 行代码)，并且是一个很好的练习。

不过有一个挑战……`outputs`脚本将在一个新进程中执行——这是 UNIX 的工作方式。这意味着它不能访问 tensorflow 图，它是在主进程中加载的。

那么如何访问张量的所有输入/输出呢？我可以在两个进程之间实现进程间通信，这是一个很大的工作量。但是我选择了不同的方法。我创建了一个包含以下行的模板 python 文件:

`_TENSOR_TO_DEPENDENCIES = {{TENSOR_TO_TENSORS_PLACEHOLDER}}`

这是非法的 python 代码。我们之前看到的`_populate_bin`函数读取这个 python 文件，并用输出(或输入)的张量字典替换`{{TENSOR_TO_TENSORS_PLACEHOLDER}}`。然后，结果文件被映射到我们的文件系统中的一个路径— `~/tf/bin/outputs`(或`~/tf/bin/inputs`)。这意味着如果您运行`cat ~/tf/bin/outputs`，您将能够看到文件内部(潜在的)巨大的映射。

# 猫。/最终想法

我们做到了！我们将张量流模型映射到文件系统。TFFS 是一个有趣的小项目，我在这个过程中了解了 FUSE，这很棒。

TFFS 是一个可爱的工具，但它不能代替旧的 python shell。使用 python，您可以轻松地导入张量流模型并手动检查张量。我只是希望我能记得如何这样做，即使在做了数百次之后…