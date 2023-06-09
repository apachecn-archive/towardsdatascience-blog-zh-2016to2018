# 为什么医院需要更好的数据科学

> 原文：<https://towardsdatascience.com/why-hospitals-need-better-data-science-7816675f4b7?source=collection_archive---------2----------------------->

![](img/aa99c664536d1a9ccb8fe963b977e34e.png)

可以说，航空公司比医院在运营上更复杂，资产更密集，监管更严格，但迄今为止，在保持低成本并获得可观利润的同时，表现最好的航空公司比大多数医院做得更好。例如，西南航空公司已经想出了如何做好最重要的两件事:让更多的飞机更频繁地停在空中，并且比任何人都更频繁地给每架飞机加油。类似地，其他复杂、资产密集型、基于服务的行业的赢家——亚马逊、运营良好的机场、UPS 和联邦快递——已经知道如何超额兑现承诺，同时保持精简和实惠。

这些例子与医疗保健有关，有两个原因。

首先，医院运营在许多方面类似于航空公司和机场运营以及运输服务。服务运营中有许多步骤(办理登机手续、行李、安检线、登机口)，每个步骤都有很高的可变性(天气延误、拥堵、机械问题)，用户旅程中有多个相互关联的环节，所有这些操作都涉及人，而不仅仅是机器。用数学术语来说，医院运营，就像航空和运输一样，由数百个小流程组成，其中每一个都比组装汽车的步骤更随机，更不确定。

第二，今天的医院面临着零售、运输和航空公司多年来面临的同样的成本和收入压力。正如西南航空、亚马逊、联邦快递和 UPS 所证明的那样，为了保持生存，资产密集型和服务型行业必须简化运营，少花钱多办事。医疗保健提供商不能通过投资越来越多的基础设施来摆脱困境；相反，他们必须优化现有资产的使用。

要做到这一点，提供商需要一如既往地做出优秀的运营决策，就像其他行业一样。最终，他们需要为他们的医院创建一个可操作的“空中交通控制”—一个具有预测性、不断学习并使用优化算法和人工智能在整个系统中提供规范性建议的集中式命令和控制能力。数十家医疗保健组织正在通过使用包括 LeanTaaS、Intelligent InSites、Qgenda、Optum 和 IBM Watson Health 在内的提供商提供的平台来简化运营。这些解决方案的共同点是能够挖掘和处理大量数据，以便向管理和临床最终用户提供建议。

通过数据科学提高医院运营效率可以归结为应用预测分析来改善关键医疗服务流程的规划和执行，其中最主要的是资源利用率(包括输液椅、手术室、成像设备和住院病床)、员工安排以及患者入院和出院。如果做得好，提供者会看到患者访问率(容纳更多患者，更快)和收入的增加、成本的降低、资产利用率的提高以及患者体验的改善。这里有几个例子:

**增加或利用。**对于一种为大多数医院带来超过 60%的入院率和 65%的收入的资源来说，当前的块调度技术在优化手术室时间和改善患者访问、外科医生满意度和护理质量方面远远不够。当前的技术—电话、传真和电子邮件—使得数据块计划的更改变得繁琐、容易出错且缓慢。利用预测分析、移动技术和云计算，提供商正在挖掘利用率模式，以大幅改善调度。

例如，移动应用程序现在允许外科医生和他们的日程安排者一键请求他们需要的封锁时间。在科罗拉多州的 UCHealth，调度应用程序允许患者更快地接受治疗(外科医生释放不需要的块的速度比手动技术快 10%)，外科医生获得更好的控制和访问(外科医生每月释放的块的中值数量增加了 47%)，整体利用率(和收入)增加。借助这些工具，UCHealth 的人均收入增加了 4%，这相当于每年增加 1500 万美元的收入。

**大幅削减输液中心等待时间。**输液调度是一个极其复杂的数学问题。即使对于一个有 30 个座位的中心来说，以病人为中心的方式避免上午 10 点到下午 2 点的“高峰时间”也需要从一个 [googol (10100)的可能解决方案中选择一个](https://www.forbes.com/sites/sanjeevagrawal/2016/08/27/the-googol-reasons-your-doctor-never-sees-you-on-time-how-data-science-has-the-answers/2/#4c39a5d54088)。面对这一挑战，纽约长老会医院应用预测分析和机器学习来优化其日程模板，从而将患者等待时间减少了 50%。除了改善长期患者排班之外，这些技术还可以帮助排班员管理输液中心的日常不确定性(最后一分钟的附加服务、延迟取消和缺席),以及优化护士的工作量和休息时间。

**简化 ED 操作。**急诊科因瓶颈而闻名，无论是因为患者在排队等待化验结果或成像，还是因为该部门人手不足。分析驱动的软件可以确定最有效的 ED 活动顺序，显著减少患者等待时间。当一名新患者需要进行 x 光检查和抽血时，了解最有效的顺序可以节省患者的时间，并更明智地利用急诊资源。软件现在可以显示历史滞留时间(也许周三 EKG 的人员短缺问题需要解决)，并实时显示每个病人在该部门的旅程和等待时间。这使得提供商能够消除反复出现的瓶颈，并呼叫工作人员或立即重新安排患者流量以提高效率。例如，埃默里大学医院使用预测分析来预测患者在一天中的时间和一周中的日期对每一类实验室测试的需求。这样，提供者将患者的平均等待时间从 1 小时减少到 15 分钟，从而相应地减少了急诊瓶颈。

**急诊转住院床位。**预测工具还可以让医疗服务提供者预测患者需要入院的可能性，并提供哪个或哪些病房可以容纳他们的即时估计。有了这些信息，住院医生和急诊医生可以很快就可能的入职流程达成一致，这可以让入职链上的每个人都可以看到。这种数据驱动的方法也有助于提供者优先考虑哪些床位应该首先清洁，哪些单元应该加速出院，以及哪些患者应该转移到出院休息室。圣地亚哥的 Sharp HealthCare 使用数据驱动的集中式患者物流系统，将其入院订单占用时间减少了三个多小时。

**加速出院计划。**为了优化出院计划，个案经理和社会工作者需要能够预见和防止出院延迟。电子健康记录或其他内部系统通常会收集有关“可避免的出院延迟”的数据，即上个月、上个季度或上一年因保险验证问题或缺乏交通工具、目的地或出院后护理而延迟的患者。这些数据对提供商来说是一座金矿；使用适当的分析工具，在患者到达并完成其文书工作的一个小时内，提供商可以相当准确地预测其数百名患者中谁最有可能在出院期间遇到麻烦。通过使用这些工具，病例管理人员和社会工作者可以创建一个高优先级患者的名单，一旦患者入院，他们就可以开始制定出院计划。例如，DC 华盛顿州的 MedStar Georgetown 大学医院使用出院分析软件，将其日出院量增加了 21%，住院时间减少了半天，并将早晨出院量增加到日出院量的 24%。

每天数百次持续做出卓越的运营决策，需要复杂的数据科学。正确使用分析工具可以降低医疗保健成本，减少等待时间，增加患者访问，并释放现有基础设施的容量。

这篇文章最初出现在[哈佛商业评论](https://hbr.org/2017/10/why-hospitals-need-better-data-science)。

***Sanjeev agr awal****是*[*LeanTaaS*](http://www.leantaas.com)*的总裁兼首席营销官。Sanjeev 是谷歌的第一任产品营销主管。从那以后，他在三家成功的初创公司担任过领导职务:移动推送平台 Aloqa 的首席执行官(被摩托罗拉收购)；Tellme Networks(已被微软收购)产品和营销副总裁；以及作为 Collegefeed(被 AfterCollege 收购)的创始 CEO。Sanjeev 毕业于麻省理工学院，获得 EECS 学位，并在麦肯锡公司和思科系统公司工作过。他是一个狂热的壁球运动员，并被贝克尔的《医院评论》评为医疗保健创新领域的顶级企业家之一。*