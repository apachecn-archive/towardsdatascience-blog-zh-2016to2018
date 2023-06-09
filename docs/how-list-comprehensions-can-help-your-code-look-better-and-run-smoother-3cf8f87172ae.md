# Python 的列表理解:用途和优点

> 原文：<https://towardsdatascience.com/how-list-comprehensions-can-help-your-code-look-better-and-run-smoother-3cf8f87172ae?source=collection_archive---------4----------------------->

![](img/7a837745736352e9d010dc855aa552fe.png)

The eyes of an interpreter, the scales of robust code. Source: [Pixabay](https://pixabay.com/en/snake-python-reptile-animal-771541/)

无论您是数据科学家、从事 API 工作的 Web 开发人员，还是一长串角色中的任何一个，您都有可能在某个时候偶然发现 Python。

我们中的一些人喜欢它的简单、流畅和易读。其他人讨厌它，因为它不像 C 或纯汇编那样高性能，具有鸭式类型，或者是单线程的(ish)。

不管你属于哪一类，如果你处于想要/必须写 Python 代码的位置，你会希望它尽可能的易读。或者你可能在野外偶然发现了一个列表理解，并对如何驯服它感到困惑。如果这些都是真的，那么这篇文章是给你的。

## 什么是列表理解？

首先，我们来定义一下我们的术语。列表理解是替代以下模式的一种句法糖:

用这个，相当于，一个:

## 为什么我们应该使用它们

使用列表理解有什么好处？首先，你将三行代码减少为一行，这对于任何理解列表理解的人来说都是显而易见的。其次，第二段代码更快，因为 Python 会先分配列表的内存，然后再添加元素，而不是在运行时调整大小。它还可以避免调用“append ”,这可能很便宜，但会增加成本。最后，使用理解的代码被认为更“Python 化”——更符合 Python 的风格准则。

## 重构代码的味道

另一个更微妙的优势是嗅觉检测。没有理解的代码可能如下所示:

如果' *some_function* '中前面或后面的代码足够长，那么关于列表的那部分可能会丢失。但是在这 6 行中直接使用列表理解看起来并不漂亮:

试图用你的眼睛来解析它会让你头疼。你们座位下面有一些纸袋，以防你们需要用。这里发生了什么事？很明显，一点逻辑应该被抽象成一个新的函数，就像这样:

refactoring with two levels of abstraction

然后，前六行代码最终只是

```
another_list = [new_function(i) for i in range(k)]
```

如果你知道发生了什么，它会更清晰(如果我没有为我们的函数取这么糟糕的名字)并且读起来更快。有些人可能会说，为了达到这个目的，我最终添加了 6 行开销代码。确实如此，但是如果这种行为在代码中至少出现了一次，那么即使这样也不算是一种损失。即使不是这种情况，我们在代码大小上的损失，我们在可维护性和易读性上的收益，这是应该追求的。

> *优秀的程序员编写人类能够理解的代码。*
> 
> ——马丁·福勒。

使用列表理解很容易做的其他事情有

## 将矩阵展开成向量:

vector_version = [1,0,0,0,1,0,0,0,1]

## 过滤列表:

## 生成一个类的许多实例(在这种情况下用一个简单的字典建模，比如 JSON 对象):

## 将某种类型的对象列表转换为另一种类型的列表:

We generate a list of the first 100 numbers turned into strings, or just a string joining them with commas. All in one smooth line!

## 性能提升

为了验证性能是否真的有所提升，我决定运行一些测试。我运行了相同代码的 for 循环版本和 list comprehension 版本，过滤和不过滤都可以。下面是测试的片段:

*list_a* 方法以通常的方式生成列表，带有 for 循环和追加。 *list_b* 方法使用列表理解。

我的结果如下:

*   列表 a 为 5.84 秒
*   名单 b 为 4.07 秒
*   过滤列表 a 为 4.85 秒
*   过滤列表 b 为 4.13 秒

我鼓励您在自己的计算机上运行同样的脚本，亲自看看性能的提升，甚至可以改变输入大小。

在未过滤的情况下，我们看到从切换到列表理解的速度提高了 33%,而过滤的算法只提高了 15%。这证实了我们的理论，即主要的性能优势来自于不必在每次迭代时调用 *append* 方法，在过滤的情况下，每隔一次迭代就跳过一次。

最后，我应该补充一点，我刚刚教你的关于列表理解的所有内容都可以用 Python 字典来完成。

## 字典理解:

这是我的列表理解速成班，我希望你喜欢它！如果有任何你觉得我应该提到而没有提到的功能，或者对 gists 有任何抱怨，请让我知道。

最后，有一本我喜欢的 O'Reilly 的书，当我开始我的数据科学之旅时，我发现它非常有用。实际上，我就是从这本书上学会理解列表的。用 Python 从零开始叫 [**数据科学，大概也是我得到这份工作的一半原因。如果你读到这里，你可能会喜欢它！**](https://www.bookdepository.com/book/9781491901427/?a_aid=strikingloo&chan=ws)

*P.S:如果你想在这个话题上展开，建议你看我的文章* [*Python 的生成器表达式*](/pythons-list-generators-what-when-how-and-why-2a560abd3879) *。我也鼓励您关注我，获取更多的 Python 教程、技巧和诀窍。*