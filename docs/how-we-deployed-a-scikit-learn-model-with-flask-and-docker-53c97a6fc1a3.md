# 我们如何使用 Flask 和 Docker 部署 scikit-learn 模型

> 原文：<https://towardsdatascience.com/how-we-deployed-a-scikit-learn-model-with-flask-and-docker-53c97a6fc1a3?source=collection_archive---------2----------------------->

在我们的上一篇文章中，我们讨论了我们的客户满意度预测模型。我们使用了 [AzureML](https://azure.microsoft.com/en-us/services/machine-learning/) studio 来首次部署这个机器学习模型，以服务于实时预测。在这篇文章中，我们将分享我们如何以及为什么使用 [Flask](http://flask.pocoo.org/) 、 [Docker](https://www.docker.com/) 和 [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/) 从 AzureML 迁移到 Python 部署。在此期间，我们还尝试了 Python 的 Azure 功能。[此外，我们开源了一个带有 Flask 和 Docker 的示例 Python API，用于机器学习](https://github.com/Soluto/python-flask-sklearn-docker-template)。

在生成我们的第一个客户满意度预测模型之后，我们希望快速、轻松地部署它。AzureML 服务于这个目的，但也表现出一些困难。我们生成的模型是使用 [scikit-learn](http://scikit-learn.org/) 开发的，但是我们部署到生产环境的模型是使用 AzureML 生成的。因此，参数并不完全相同，我们测量的一些指标也不同。此外，我们有一些数据准备逻辑，由模型训练和实时预测共享，但在代码方面是重复的。最后，我们发现 AzureML GUI 非常慢，因此对用户不太友好。

从上述问题中，我们得出了对第二个预测模型部署架构的以下要求:

*   快速简单的部署
*   在本地环境中培训的相同模型可以部署到生产中
*   在生产和模型培训之间共享数据准备代码
*   轻松的端到端流量控制
*   不是必须的:易于集成到持续部署中(例如 [codefresh](https://codefresh.io/) )

首先，我们尝试在 Python 中使用 Azure Function rest API。设置非常简单，我们很快就能运行 Python 代码。此外，使用 [Kudu](https://github.com/projectkudu/kudu) 也很容易、快速且非常用户友好。虽然它显示了希望，但后来事情变得更加困难:

*   在 Windows 机器上安装机器学习的库更难一些——一些基本的库，如 [NumPy](http://www.numpy.org/) 需要特殊处理，然后只是“pip 安装”
*   Azure 函数在每个请求上运行所有的导入，在我们的情况下(numpy，scikit-learn，pandas)导入花费了大约 30 秒(更多细节请参见这个[问题](https://github.com/Azure/azure-webjobs-sdk-script/issues/1626))——这对我们来说是一个障碍

最后，我们决定尝试部署我们自己的服务器，使用:

*   flask:Python 的微型网络框架，非常容易设置
*   码头工人
*   Azure 应用服务

我们从中获得了什么:

*   由于我们部署了自己的服务器，我们有了完整的端到端控制——这使得实时 API 和离线模型训练之间的代码共享变得容易
*   使用 [Pickle](https://docs.python.org/3/library/pickle.html) 将离线训练的实际模型部署到生产中
*   由于 Docker 运行在 Linux 虚拟机上，不再有 Windows“pip 安装”的困难
*   Docker 使这项服务可以在多个平台上托管——如果 Azure 应用服务出现问题，迁移将非常容易
*   从源代码 git 存储库到 codefresh 的轻松集成——这处理了我们所有的持续部署过程——每次提交到我们的 git 存储库都会将新代码部署到一个辅助服务，该服务可以轻松地转换为我们的主要实时服务

顺便说一下，Azure 对 Docker 的应用服务支持仍处于预览阶段――更多信息可以在这里找到。

想试试吗？

[可在此处找到 docker 图像样本](https://hub.docker.com/r/soluto/python-flask-sklearn-docker-template/)

[可以在这里找到该架构的代码示例](https://github.com/Soluto/python-flask-sklearn-docker-template)

在下一篇文章中，我们将分享更多关于我们新系统架构的实时性能、将会出现的新问题(总是有问题:-)，以及更多关于我们新挑战和新特性的内容。