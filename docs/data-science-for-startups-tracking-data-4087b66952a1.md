# 创业公司的数据科学:跟踪数据

> 原文：<https://towardsdatascience.com/data-science-for-startups-tracking-data-4087b66952a1?source=collection_archive---------4----------------------->

![](img/354cdb973d13facd3abdf701b842f967.png)

Source: kristinakasp at pixabay.com

我正在进行的关于在初创公司建立数据科学学科的系列文章的第二部分。你可以在 [*简介*](/data-science-for-startups-introduction-80d022a18aec) *中找到所有帖子的链接，还有一本基于这个系列的关于* [*亚马逊*](https://www.amazon.com/dp/1983057975) *的书。*

为了在创业时做出数据驱动的决策，你需要收集关于你的产品如何被使用的数据。您还需要能够衡量产品变更的影响以及营销活动的效果，例如在脸书上部署定制受众进行营销。同样，收集数据对于实现这些目标是必要的。

通常数据是由产品直接生成的。例如，移动游戏可以生成关于启动游戏、开始附加会话和升级的数据点。但是数据也可以来自其他来源，例如电子邮件供应商提供关于哪些用户阅读和点击了电子邮件中的链接的响应数据。这篇文章主要关注第一种类型的数据，即产品生成的跟踪事件。

为什么要记录产品使用数据？

1.  **跟踪指标:**您可能希望记录绩效指标，以跟踪产品健康状况或其他对业务运营有用的指标。
2.  **进行实验:**为了确定对产品进行改变是否有益，你需要能够衡量结果。
3.  **构建数据产品:**为了做出类似推荐系统的东西，你需要知道用户在和哪些项目进行交互。

有人说数据是新的石油，有各种各样的理由从产品中收集数据。当我刚开始进入游戏行业时，从产品跟踪的数据被称为 [*遥测*](https://www.gdcvault.com/play/1012227/Development-Telemetry-in-Video-Games) 。现在，从产品中收集的数据经常被称为*跟踪*。

这篇文章讨论了收集什么类型的产品使用数据，如何将数据发送到服务器进行分析，构建跟踪 API 时的问题，以及跟踪用户行为时需要考虑的一些问题。

## 录什么？

部署新产品时首先要回答的问题之一是:

> 关于用户行为，我们应该收集哪些数据？

答案是，这取决于您的产品和预期的用例，但有一些关于在大多数 web、移动和本机应用程序中收集什么类型的数据的通用指南。

1.  **安装:**用户基数有多大？
2.  **会议:**用户群的参与度如何？
3.  **货币化:**用户花了多少钱？

对于这三种类型的事件，数据可能实际上是从三个不同的系统生成的。安装数据可能来自第三方，如 Google Play 或 App Store，会话开始事件将从客户端应用程序生成，在应用程序中花钱或查看广告可能会被不同的服务器跟踪。只要您拥有生成数据点的服务，就可以使用相同的基础设施来收集不同类型事件的数据。

收集关于有多少用户启动和登录应用程序的数据将使您能够回答关于您的基础规模的基本问题，并使您能够跟踪业务指标，如 DAU、MAU、ARPDAU 和 D-7 保留率。然而，它没有提供太多关于用户在应用程序中正在做什么的信息，也没有提供许多对构建数据产品有用的数据点。为了更好地了解用户参与度，有必要跟踪特定领域或产品的数据点。例如，您可能希望在控制台的多人射击游戏中跟踪以下类型的事件:

1.  **GameStarted:** 追踪玩家何时开始单人或多人游戏。
2.  **PlayerSpawn:** 追踪玩家何时产卵进入游戏世界，并追踪用户正在玩的职业，比如战斗医疗兵。
3.  **玩家死亡:**追踪玩家死亡和卡住的地方，并允许计算指标，如 KDR(杀死/死亡比率)。
4.  **等级:**追踪玩家升级或解锁新等级的时间。

这些事件中的大多数可以很好地转化为其他射击游戏和其他类型，如动作/冒险。对于特定的游戏，例如 FIFA，您可能希望记录游戏特定的事件，例如:

1.  **进球得分:**追踪球员或对手得分的时间。
2.  **球员替换:**跟踪球员何时被替换。
3.  **RedCardReceived:** 追踪玩家何时收到红牌。

像先前的事件一样，许多这些游戏特有的事件实际上可以推广到体育游戏。如果你是一家像 e a 这样的公司，拥有不同的体育项目组合，那么在你所有的体育项目中跟踪所有这些事件是很有用的(红牌事件可以概括为点球事件)。

如果我们能够收集关于玩家的这些类型的事件，我们就可以开始回答关于玩家基础的有用问题，例如:

1.  收到更多红牌的用户更有可能退出吗？
2.  在线专注玩家比单机专注玩家玩的多吗？
3.  用户玩的是刚发布的新职业模式吗？

大多数跟踪事件都集中在收集已发行游戏的数据点上，但也有可能在开发过程中收集数据。在微软工作室，我与用户研究团队合作，为游戏测试进行跟踪。因此，我们可以生成可视化效果，用于向游戏团队传达玩家遇到的困难。将这些可视化整合到游戏测试结果中，会得到游戏团队更好的接受。

![](img/570228694e617ef398f0de021818eab2.png)

Ryse: Son of Rome Playtesting — Microsoft Studios User Research

当您第一次将跟踪添加到产品中时，您不会知道对记录有用的每一个事件和属性，但是您可以通过询问团队成员他们打算问什么类型的关于用户行为的问题，以及通过实现能够回答这些问题的事件来做出一个很好的猜测。即使有好的跟踪数据，你也不可能回答每个问题，但是如果你有好的覆盖率，你就可以开始改进你的产品。

## 跟踪规格

一些团队编写跟踪规范来定义产品中需要实现的跟踪事件。其他团队没有任何文档，只是简单地采用最佳猜测方法来确定记录什么。我强烈推荐编写跟踪规范作为最佳实践。对于每个事件，规范应该确定触发事件的条件、要发送的属性以及任何特定于事件的属性的定义。例如，web 应用程序的会话启动事件可能具有以下形式:

*   **条件:**当用户第一次浏览到该域时触发。当用户点击新页面或使用后退按钮时不应触发该事件，但当用户浏览到一个新的域并返回时应触发该事件。
*   **属性:**网络浏览器和版本、用户标识、登陆页面、引用 URL、客户端时间戳
*   **定义:** referring URL 应列出将用户推荐到该域的页面的 URL，或者将用户推荐到该网页的应用程序(如脸书或 Twitter)。

跟踪规格是非常有用的文档。小型团队可能没有编写跟踪规范的正式过程，但是许多场景会使文档变得至关重要，例如在新平台上实现事件，为新的后端服务重新实现事件，或者让工程师离开团队。为了使规格有用，有必要回答以下问题:

1.  谁负责编写规范？
2.  谁负责实施规范？
3.  谁负责测试实现？

在小型组织中，数据科学家可能负责跟踪的所有方面。对于一个更大的组织，所有者通常是产品经理、工程团队和测试团队。

## 客户端与服务器跟踪

为产品设置跟踪时的另一个考虑是确定是从客户端应用程序还是后端服务发送事件。例如，一个视频流网站可以直接从 web 浏览器或者从提供视频的后端服务发送关于用户正在观看的视频的数据。虽然这两种方法各有利弊，但如果可能的话，我更喜欢为后端服务而不是客户端应用程序设置跟踪。服务器端跟踪的一些好处是:

1.  **可信来源:**您不需要在 web 上公开端点，并且您知道事件是从您的服务而不是机器人生成的。这有助于避免欺诈和 DDoS 攻击。
2.  **避免广告拦截:**如果您将数据从客户端应用程序发送到暴露在 web 上的端点，一些用户可能会阻止对端点的访问，这会影响业务指标。
3.  **版本化:**你可能需要对一个事件进行修改。您可以根据需要更新 web 服务器，但通常不能要求用户更新客户端应用程序。

从服务器而不是客户端应用程序生成跟踪有助于避免欺诈、安全和版本控制方面的问题。然而，服务器端跟踪有一些缺点:

1.  **测试:**出于测试目的，您可能需要添加新的事件或者修改现有的跟踪事件。这通常更容易通过在客户端进行更改来实现。
2.  **数据可用性:**您可能想要跟踪的一些事件不会调用 web 服务器。例如，一个控制台游戏可能在会话开始时没有连接到任何 web 服务，而是希望直到多人游戏比赛开始。此外，诸如引用 URL 之类的属性可能只对客户端应用程序可用，而对后端服务不可用。

一般原则是不要相信客户端应用程序发送的任何内容，因为端点通常是不安全的，并且没有办法验证数据是由您的应用程序生成的。但是客户端数据非常有用，所以最好将客户端和服务器端跟踪结合起来，并保护用于从客户端收集跟踪的端点。

## 发送跟踪事件

向服务器发送数据的目的是使数据可用于分析和数据产品。根据您的使用案例，可以使用许多不同的方法。本节介绍了向 web 上的端点发送事件并将事件保存到本地存储的三种不同方式。下面的示例不是产品代码，而是简单的概念证明。本系列的下一篇文章将讨论构建处理事件的管道。以下示例的所有代码都可以在 [Github](https://github.com/bgweber/StartupDataScience/tree/master/TrackingData) 上获得。

**网络呼叫** 建立追踪服务最简单的方法是通过网络呼叫网站的事件数据。这可以用一个轻量级 PHP 脚本来实现，如下面的代码块所示。

```
<?php
    $message = $_GET['message'];
    if ($message != '') {
        $dataFile = fopen("telemetry.log", "a");
        fwrite($dataFile, "$message\n");
        fflush($dataFile);
        fclose($dataFile);
    }
?>
```

这个 php 脚本从 URL 中读取消息参数，并将消息附加到本地文件中。可以通过 web 调用来调用该脚本:

```
http://.../tracking.php?message=Hello_World
```

可以使用下面的[代码](https://github.com/bgweber/StartupDataScience/blob/master/TrackingData/WebCall/SendEvent.java)从 Java 客户端或服务器进行调用:

```
// endpoint
String endPoint = "http://.../tracking.php";// send the message
String message = "Hello_World_" + System.currentTimeMillis();   
URL url = new URL(endPoint + "?message=" + message);  
URLConnection con = url.openConnection();  
BufferedReader in = new BufferedReader(new 
    InputStreamReader(con.getInputStream())); // process the response 
while (in.readLine() != null) {}  
in.close();
```

这是开始收集跟踪数据的最简单的方法之一，但它不可扩展，也不安全。这对于测试很有用，但是对于任何面向客户的东西都应该避免使用。我过去确实用这种方法为一个马里奥[级别的生成器实验](http://www.gamasutra.com/blogs/BenWeber/20131228/207819/Adding_Telemetry_to_Infinite_Mario.php)收集玩家的数据。

**Web 服务器** 您可以使用的另一种方法是建立一个 Web 服务来收集跟踪事件。下面的代码展示了如何使用 [Jetty](http://www.eclipse.org/jetty/) 来建立一个收集数据的轻量级服务。为了编译和运行这个例子，您需要包含下面的 [pom 文件](https://github.com/bgweber/StartupDataScience/blob/master/TrackingData/WebService/pom.xml)。第一步是启动一个处理跟踪请求的 web 服务:

```
public class TrackingServer extends AbstractHandler { public static void main(String[] args) throws Exception {
    Server server = new Server(8080);
    server.setHandler(new TrackingServer());
    server.start();
    server.join();
  } public void handle(String target, Request baseRequest,
      HttpServletRequest request, HttpServletResponse response) 
      throws IOException, ServletException { // Process Request
  }
}
```

为了处理事件，应用程序从 web 请求中读取消息参数，将消息附加到本地文件，然后响应 web 请求。此示例的完整代码可从[这里](https://github.com/bgweber/StartupDataScience/blob/master/TrackingData/WebService/TrackingServer.java)获得。

```
// append the event data to a local file 
String message = baseRequest.getParameter("message");
if (message != null) {
  BufferedWriter writer = new BufferedWriter(
      new FileWriter("tracking.log", true));
  writer.write(message + "\n");
  writer.close();
}// service the web request
response.setStatus(HttpServletResponse.SC_OK);
baseRequest.setHandled(true);
```

为了用 Java 调用端点，我们需要修改 URL:

```
URL url = new URL("[http://localhost:8080/](http://localhost:8080/?message=Hello_World)?message=" + message);
```

这种方法可以比 PHP 方法扩展得多一点，但是仍然不安全，不是构建生产系统的最佳方法。我对构建生产就绪跟踪服务的建议是使用流处理系统，如 Kafka、Amazon Kinesis 或 Google 的 PubSub。

**订阅服务** 使用 PubSub 等消息服务使系统能够收集大量的跟踪数据，并将这些数据转发给许多不同的消费者。Kafka 等一些系统需要设置和维护服务器，而 PubSub 等其他方法是无服务器的托管服务。托管服务非常适合初创公司，因为它们减少了所需的开发运维支持量。但是代价是成本，使用托管服务来收集大量数据的成本更高。

下面的代码展示了如何使用 Java 向 PubSub 上的主题发布消息。完整的代码清单可从[这里](https://github.com/bgweber/StartupDataScience/blob/master/TrackingData/SubscriptionService/SendEvent.java)获得，用于构建项目的 pom 文件可从[这里](https://github.com/bgweber/StartupDataScience/blob/master/TrackingData/SubscriptionService/pom.xml)获得。为了运行这个例子，您需要建立一个免费的 google cloud 项目，并启用 PubSub。关于设置 GCP 和 PubSub 的更多细节可以在[这篇文章](/a-simple-and-scalable-analytics-pipeline-53720b1dbd35)中找到。

```
// Set up a publisher
TopicName topicName = TopicName.of("projectID", "raw-events");
Publisher publisher = Publisher.newBuilder(topicName).build();//schedule a message to be published
String message = "Hello World!";
PubsubMessage pubsubMessage = PubsubMessage.newBuilder()
    .setData(ByteString.copyFromUtf8(message)).build();// publish the message, and add this class as a callback listener
ApiFuture<String> future = publisher.publish(pubsubMessage);
ApiFutures.addCallback(future, new ApiFutureCallback<String>() {
  public void onFailure(Throwable arg0) {}
  public void onSuccess(String arg0) {}
});publisher.shutdown();
```

此代码示例显示了如何向 PubSub 发送一条消息来记录跟踪事件。对于一个生产系统，您将希望实现 *onFailure* 方法来处理失败的交付。上面的代码显示了如何用 Java 发送消息，同时也支持其他语言，包括 Go、Python、C#和 PHP。它还可以与其他流处理系统(如 Kafka)连接。

下一段代码显示了如何从 PubSub 读取消息，并将消息附加到本地文件。完整的代码清单可在[这里](https://github.com/bgweber/StartupDataScience/blob/master/TrackingData/SubscriptionService/ReadEvent.java)获得。在下一篇文章中，我将展示如何使用数据流消费消息。

```
// set up a message handler
MessageReceiver receiver = new MessageReceiver() {
  public void receiveMessage(PubsubMessage message, 
    AckReplyConsumer consumer) { try {
      BufferedWriter writer = new BufferedWriter(new
        FileWriter("tracking.log", true));
      writer.write(message.getData().toStringUtf8() + "\n");
      writer.close();
      consumer.ack();
    }
    catch (Exception e) {}
}};// start the listener for 1 minute
SubscriptionName subscriptionName =
    SubscriptionName.of("your_project_id", "raw-events");
Subscriber subscriber = Subscriber.newBuilder(
    subscriptionName, receiver).build();
subscriber.startAsync();
Thread.sleep(60000);
subscriber.stopAsync();
```

我们现在有了一种从客户端应用程序和后端服务获取数据到一个中心位置进行分析的方法。显示的最后一种方法是用于收集跟踪数据的可扩展且安全的方法，并且是一种托管服务，使其非常适合具有小型数据团队的初创公司。

## 消息编码

将数据发送到端点进行收集时，需要做出的决策之一是如何对发送的消息进行编码，因为从应用程序发送到端点的所有事件都需要序列化。当通过互联网发送数据时，最好避免特定语言的编码，比如 Java 序列化，因为应用程序和后端服务可能用不同的语言实现。当使用特定于语言的序列化方法时，还会出现版本控制问题。

编码跟踪事件的一些常见方法是使用 [JSON 格式](http://www.json.org/)和谷歌的[协议缓冲区](https://developers.google.com/protocol-buffers/)。JSON 的优点是可读性强，并且受到多种语言的支持，而 buffers 提供了更好的理解，可能更适合某些数据结构。使用这些方法的好处之一是在发送事件之前不需要定义模式，因为消息中包含了关于事件的元数据。您可以根据需要添加新的属性，甚至更改数据类型，但这可能会影响下游的事件处理。

当开始构建数据管道时，我推荐使用 JSON 开始，因为它是人类可读的，并且受到多种语言的支持。避免管道分隔格式之类的编码也很好，因为在更新跟踪事件时，您可能需要支持更复杂的数据结构，如列表或地图。下面是一个消息的示例:

```
# JSON
{"Type":"Session","Version":1.0,"UserID":"12345","Platform":"iOS"}# Pipe delimited
Session|1.0|12345|iOS
```

XML 呢？不要！

## 构建跟踪 API

要构建一个生产系统，您需要在跟踪代码中增加一点复杂性。生产系统应该处理以下问题:

1.  **传递失败:**如果消息传递失败，系统应该重试发送消息，并有退避机制。
2.  **排队:**如果端点不可用，比如没有信号的电话，跟踪库应该能够存储事件以供以后传输，比如当 wifi 可用时。
3.  **批处理:**与其发送大量的小请求，不如批量发送跟踪事件。
4.  **优先级:**有些消息比其他消息更需要跟踪，比如更喜欢货币化事件而不是点击事件。跟踪库应该能够优先处理更关键的事件。

拥有一个禁用跟踪事件的过程也很有用。我见过客户端应用程序发送太多数据导致数据管道爆炸，如果不关闭所有跟踪，就无法禁止客户端发送有问题的事件。

理想情况下，生产级系统应该有某种审计，以便验证端点是否接收到所有发送的数据。一种方法是将数据发送到构建在不同基础设施和跟踪库上的不同端点，但是过多的冗余通常是多余的。一种更轻量级的方法是为所有事件添加一个顺序计数属性，因此如果一个客户端发送 100 条消息，后端可以使用这个属性来知道客户端尝试发送了多少个事件并验证结果。

## 隐私

存储用户数据时需要考虑隐私问题。当数据可供分析和数据科学团队使用时，所有个人身份信息(PII)都应该从事件中剔除，包括姓名、地址和电话号码。在某些情况下，用户名，如玩家在 Steam 上的玩家代号，也可能被视为 PII。从任何被收集的数据中去除 ip 地址也是很好的，以限制隐私问题。一般建议是收集尽可能多的行为数据来回答有关产品使用的问题，同时避免收集敏感信息，如性别和年龄。如果你正在基于敏感信息构建一个产品，你应该有强有力的用户访问控制来限制对敏感数据的访问。GDPR 等政策正在为收集和处理数据制定新的法规，GDPR 在运送带跟踪功能的产品前应接受审查。

## 摘要

跟踪数据使团队能够回答关于产品使用的各种问题，使团队能够跟踪产品的性能和健康状况，并可用于构建数据产品。这篇文章讨论了收集用户行为数据所涉及的一些问题，并提供了如何将数据从客户端应用程序发送到端点以供以后分析的示例。以下是这篇文章的要点:

1.  如果可能，使用服务器端跟踪。它有助于避免各种各样的问题。
2.  QA/测试您的跟踪事件。如果你发送的是错误的数据，你可能会从数据中得出不正确的结论。
3.  有一个版本控制系统。您需要添加新事件和修改现有事件，这应该是一个简单的过程。
4.  使用 JSON 发送事件。它是人类可读的、可扩展的，并且受到多种语言的支持
5.  使用托管服务收集数据。你不需要启动服务器，就可以收集大量的数据。

随着您运送更多的产品和扩大您的用户群，您可能需要更改到不同的数据收集平台，但此建议是运送带跟踪的产品的良好起点。

*下一篇文章将介绍构建数据管道的不同方法。*

[本·韦伯](https://www.linkedin.com/in/ben-weber-3b87482/)是游戏行业的数据科学家，曾在电子艺界、微软工作室、黎明游戏和 Twitch 任职。他还在一家金融科技初创公司担任第一位数据科学家。