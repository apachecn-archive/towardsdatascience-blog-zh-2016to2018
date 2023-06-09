# MongoDB——引领 NoSQL 的潮流

> 原文：<https://towardsdatascience.com/mongodb-world-18-leading-the-nosql-charge-b6032116f31f?source=collection_archive---------13----------------------->

## MongoDB World’18 向我们展示了数据库技术的未来

![](img/dc9dc85b0092633c1b76433f381eecbb.png)

CTO Eliot Horowitz introduced many of the novel features of MongoDB 4.0.

你好。我是 Sohan。欢迎来到我的第一篇博客。我的目标是利用这个空间，通过我自己作为计算机科学本科生的成长来探索科技世界。我决定从 MongoDB 开始，这是因为它给这个行业带来了创新，也是因为我接触了这个产品。

6 月 27 日星期三，我有机会前往纽约参加 MongoDB World 2018。在该公司的旗舰年度会议上，MongoDB 4.0 被公布，同时还有许多功能可以帮助公司永远转向非关系数据库。

![](img/b3970b47839c7df0b4a1068adca02a67.png)

Example of a collection of JSON documents. ([s*ource*](https://docs.mongodb.com/manual/core/databases-and-collections/)*)*

那么，什么是非关系(或 NoSQL)数据库呢？嗯，它们与关系数据库有很大的不同，这是一个很好的复习，可以在这里找到。MySQL 等传统数据库利用基于表的结构来存储数据，而在非关系型数据库中，一切都是基于文档的。文档以无序的方式存储在一个集合中，通常没有什么层次结构。每个文档都代表一个对象—无论是客户还是待售商品—并且具有任何和所有相应的信息—从名称和年龄到价格和剩余库存。这为数据存储提供了更大的灵活性，并减少了手动构建数据所花费的时间和精力。

越来越多的公司决定转向非关系数据库，尽管 MongoDB 在 2009 年才推出，但它在最受欢迎的数据库中排名第五。街区里新来的孩子正在获得大量的街头信誉，这并不奇怪为什么。凭借更快的数据访问速度、出色的可伸缩性和熟悉的 JSON 风格文档(更不用说专业的 MongoDB 支持)，这些优势在大数据时代显而易见。我在 [Everbridge](https://medium.com/team-everbridge) 的暑期实习中一直在使用 MongoDB，我可以证明它的易用性和快速查询。

目前，MongoDB 面临的最大挑战包括扩大客户群和让用户为优质服务付费。作为一个开源产品，MongoDB 的商业模式建立在开发者和支持特性的基础上，这使得客户获取和保持对其成功至关重要。这一重点在首席执行官 Dev Ittycheria 上台的会议主基调上非常明显。在谈到该公司最近的快速增长(以及 2017 年 10 月 IPO 后股价飙升)后，他将注意力转移到了客户故事上。Travelers Insurance、Braze 和比特币基地等公司的高管和开发人员走上舞台，讨论如何使用 MongoDB，特别是该公司的优质云服务产品 Atlas，通过满足业务需求来帮助支持快速增长。

Hyman explained how MongoDB’s scalability has helped Braze send billions of notifications to customers.

对客户故事的巨大关注绝对让我大吃一惊。总而言之，Ittycheria 在很大程度上充当了一个主持人的角色，他很好地设计了各种各样的评价。从房间的气氛来看，这种方法显然是合格的。几乎每个我在会议上交谈过的人似乎都对这个产品感到由衷的兴奋。顾客故事无处不在——itty cheria 只是选择了最有影响力的故事。从初创公司的创始人到辉瑞或 IBM 等传统公司的员工，很明显，MongoDB 是一股不断增长的受欢迎的颠覆力量。

随着 MongoDB 4.0 的现场发布，这种兴奋感更加强烈了。在主题演讲的这一部分，首席技术官兼联合创始人艾略特·霍洛维茨率先发言，没有让大家失望。他将矛头直接指向传统数据库，开玩笑地将 SQL 称为“低劣的查询语言”，并公开了显然旨在处理关系数据库优势的特性。

![](img/8be9e00dd974acb0926e05436d4acd31.png)

MongoDB’s evolution has been driven towards Multi-Documented Transactions with the goal of improving data integrity. ([source](https://www.mongodb.com/blog/post/multi-document-transactions))

有什么新鲜事吗？4.0 的主要好处是它为 MongoDB 带来了 ACID(原子的、一致的、隔离的、持久的)事务，并且以一种非关系数据库闻所未闻的方式。为什么这很重要？我将借用霍洛维茨提供的一个案例，并做一些修改。

假设你有一个网上商店，在那里你出售纪念品来支持你最喜欢的当地足球队。有了 MongoDB 4.0 的交易，你所有的库存都会随着订单的到来而被准确跟踪。例如，如果一个客户从您的网站订购了一件 35 美元的运动衫，在一次交易中，客户的总额将增加 35 美元，而您的该运动衫的可用库存将减少一件。以前，事务中的故障(通常由网络故障或服务器崩溃引起)会导致重大问题，而多文档 ACID 可以防止这种情况。

在欧洲有铁杆支持者，只需要得到那些个性化的帽子？Atlas 的全球集群允许您将他们的数据放在您需要的地理位置，然后您可以在那里读取和写入，从而有助于 GDPR 合规性。通过 AWS、微软 Azure 和谷歌云平台的可用性，有丰富多样的服务器位置可供选择。

![](img/881ac07c98ca6efddee44bc5f28c7be6.png)

对于我们的案例来说，这就足够了。这一切对你来说意味着什么？

早些时候，我将 MongoDB 描述为一股受欢迎的不断增长的颠覆力量。那是有条件的真实。为了真正欢迎这些变化，必须了解非关系技术及其在塑造数据使用和存储的未来方面的进步。在这个不断变化的行业中保持最新。资源就在那里！

MongoDB 已经在教育领域取得了长足的进步——查看 [MongoDB 大学](https://university.mongodb.com)的官方在线课程和来源认证。对于定期的技术博客帖子，你知道在哪里可以找到我。谢谢你的来访！