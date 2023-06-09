# 如何建立简单的线性回归模型？

> 原文：<https://towardsdatascience.com/linear-regression-model-899558ba0fc4?source=collection_archive---------2----------------------->

这篇文章是关于一步一步地为 ML 初学者实现简单的线性回归模型，并有详细的解释。

如果你是机器学习的新手，请查看 [***这篇***](https://medium.com/@diti.modi/machine-learning-simplified-3f964c1a64a6) 的帖子，了解机器学习及其基础知识。

**简单线性回归模型背后的逻辑是什么？**

顾名思义，线性回归遵循从一个给定自变量的值确定一个因变量的值的线性数学模型。还记得学校里的线性方程吗？

# y=mx+c

其中 y 是因变量，m 是斜率，x 是自变量，c 是给定直线的截距。

我们也有多元回归模型，其中多个自变量用于计算一个因变量。

我已经用 Jupyter 笔记本实现了。您可以选择使用任何 Python IDE 所以让我们开始吧..

步骤 1:导入库

![](img/b760960fee1b77429f18ffd6176ff70f.png)

Step 1

Python 中已经开发了用于实现机器学习模型的库。

第一个名为 matplotlib 的库用于在最后一步绘制图形。“plt”用作变量名，用于在前面的代码中使用该库。

sklearn 是 python 中的官方机器学习库，用于各种模型实现。

numpy 用于将数据转换成数组，供 sklearn 库实际使用。

熊猫是用来访问的。数据集的 csv 文件。

步骤 2:加载数据集

![](img/6672c1a50c1f5797dd92086c171f3a3a.png)

我们的数据集是. csv 文件类型。Pandas 变量 pd 用于通过 read_csv()函数访问数据集。

第三步:分解为自变量和因变量

![](img/7783a10d0fcc103a2c7b58e25db52376.png)

我们通过 iloc(索引位置)值定义 x 为数据集中的自变量。[]用于定义数组元素。":"[]内表示考虑数据集中的所有行，并使用" "分隔。我们指定要用作自变量或因变量的列数，从数据集中的零开始计数。

步骤 4:将数据分为训练数据和测试数据

![](img/d4e091deeb0a519a708e52739c2a839f.png)

现在，整个数据集被分为训练集和测试集，这样预测就不会过拟合或欠拟合，从而获得正确值。train_test_split()是 scikit learn 的内置函数，用于拆分 x 和 y 变量数据。“test_size”参数用于将整个数据集(30%)的 1/3 划分为测试数据，其余部分作为训练数据。将 random_state 设置为 null 将不允许从数据集中获取随机值。

第五步:选择模型

![](img/0096e7effbeced1086c7ee8c7e08ade0.png)

我们重塑我们的自变量，因为 sklearn 期望一个 2D 数组作为输入。

这里的线性回归是我们的模型，模型的变量名为“lin_reg”。我们也可以用许多其他模型来尝试相同的数据集。该部分因型号而异，否则所有其他步骤都与此处描述的相似。

第六步:符合我们的模型

![](img/6839cd1f694f3595494e6ecccf081327.png)

现在，我们通过用自变量和因变量训练模型，使我们的模型适合线性回归模型。

第七步:预测输出

![](img/bfd197481f36432301281baeeef45d28.png)

最后，我们的模型使用自变量的测试值来预测因变量“lin_reg_pred”。

我们可以看到异常值的系数、截距值，以及预测值(lin_reg_pred)和因变量的实际测试值(y_test)的均方误差和方差。内置方法使用预定义的公式计算每个值。

第八步:绘制图表

![](img/f1ddff7c83a25acdeb2cece811823029.png)

我们最终希望以图形格式可视化实际数据值和预测数据值。matplotlib 变量“plt”用于使用“scatter()”绘制点，使用“plot()”函数绘制异常值。

输出可能因不同的系统功能而异。我得到的输出如下:

![](img/95125fef0f7708b9dc219b9a1255a103.png)

Output

![](img/9b6d94c8301d2557206312ecf8c05e76.png)

Output Graph

就是这个！我们的第一个线性回归模型实现了！下面是我们在这里实现的整个模型的完整代码的链接。

[](https://github.com/ditsme/MachineLearning) [## ditsme/机器学习

### 机器学习——我所有的机器学习项目

github.co](https://github.com/ditsme/MachineLearning) 

在 LinkedIn 上关注我:[www.linkedin.com/comm/mynetwork/discovery-see-all?use case = PEOPLE _ FOLLOWS&follow member = dit modi](http://www.linkedin.com/comm/mynetwork/discovery-see-all?usecase=PEOPLE_FOLLOWS&followMember=ditimodi)