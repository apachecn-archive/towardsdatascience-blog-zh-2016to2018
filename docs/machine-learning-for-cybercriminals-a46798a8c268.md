# 网络罪犯的机器学习 101

> 原文：<https://towardsdatascience.com/machine-learning-for-cybercriminals-a46798a8c268?source=collection_archive---------4----------------------->

![](img/a7437a35ab152d9ec5de88d17c60ac7c.png)

ID 78201212 © Juan Moyano | Dreamstime.com

机器学习(ML)和人工智能(AI)正在网络安全和其他技术领域掀起风暴，你可以很容易地找到大量关于防御和网络攻击两个阵营使用 ML 的信息。

***更重要的是，AI 也不能免疫攻击，你可以在这里阅读***[](/ai-and-ml-security-101-6af8026675ff)****我的新文章。****

*将机器学习用于网络攻击仍不明确。然而，2016 年，美国情报界对人工智能的部署提出了担忧，对网络安全构成了潜在威胁。最近的发现证明了机器学习如何被网络犯罪分子用于更高级、更快和更便宜的攻击。*

*虽然我以前的文章“[网络安全的机器学习 101](/machine-learning-for-cybersecurity-101-7822b802790b) ”详细介绍了防御的人工智能，但现在是时候轮到网络罪犯的机器学习了。在这里，我对恶意网络空间中机器学习部署的可能或现有方法的信息进行了系统化。本文旨在帮助信息安全团队为即将到来的威胁做好准备。*

# *网络罪犯的任务*

*攻击者的活动分为 5 组机器学习可以解决的高级任务。*

1.  *信息收集——为攻击做准备；*
2.  *模仿——试图模仿知己；*
3.  *未经授权的访问—绕过限制获得对某些资源或用户帐户的访问权；*
4.  *攻击——执行恶意软件或 DDoS 等实际攻击；*
5.  *自动化—自动化开发和后期开发。*

# *用于信息收集的机器学习*

*无论受害者人数多少，信息收集都是每一次网络攻击的第一步。你收集的信息越多，你成功的前景就越好。*

*信息可以按科目分组整理，可以线上收集，也可以线下收集。信息可以指人或资产。让我们看看所有这些类别。*

# *ML 用于收集网上人们的信息*

*在网络钓鱼或感染准备的情况下，黑客可以使用分类算法将潜在受害者描述为属于相关组。这意味着在收集了数千封电子邮件后，黑客只向那些点击链接的人发送恶意软件。因此，攻击者减少了及早发现计划攻击的机会。许多因素可能有助于此。例如，黑客可以将写博客的社交网站用户与关注“食物和猫”话题的用户区分开来。后一组人可能没有意识到威胁。*

*在这种情况下，除了 NLP 分析之外，还可以使用从 K-means 和随机森林到神经网络的各种聚类和分类方法，这些方法应该应用于受害者在社交网络上的帖子。*

*其他类型的分类可以与受害者的偿付能力有关。第一个受害者检测算法将针对穿着品牌服装的用户，例如，穿着巴黎世家鞋和最新古驰包在私人飞机上拍照的孩子。*

*这是网络罪犯没有特定目标的信息收集的一个例子。如果攻击者认识受害者并有他或她的照片，ML 可以进一步协助。通过应用图像识别工具，很容易检测社交媒体账户。Trustwave 已经通过其名为 [Social Mapper](https://www.trustwave.com/Resources/SpiderLabs-Blog/Mapping-Social-Media-with-Facial-Recognition--A-New-Tool-for-Penetration-Testers-and-Red-Teamers/?page=1&year=0&month=0&LangType=1033) 的工具迈出了自动化的第一步，该工具旨在不同的社交媒体平台中搜索一个人。这个解决方案使用谷歌图片搜索。*

*我敢打赌，类似于真实图像识别的功能很快就会被开发出来。*

*![](img/f6a1e3683cd29a65053957cd687b49b1.png)*

# *ML 用于收集有关在线 IT 资产的信息*

*有针对性的攻击的信息收集处理一个受害者和复杂的基础设施。目标是收集尽可能多的关于这个基础设施的信息。*

*这个想法是自动检查，包括收集有关网络的信息。虽然网络扫描器和嗅探器等现有工具能够分析传统网络，但基于软件定义网络(SDN)的新一代网络过于复杂。这就是机器学习可以帮助对手的地方。一个鲜为人知但很有用的[了解你的敌人](https://arxiv.org/abs/1608.04766) (KYE)攻击允许秘密收集关于目标 SDN 网络配置的情报，这是将机器学习应用于信息收集任务的一个相关示例。黑客可以收集这些信息，范围从安全工具和网络虚拟化参数的配置到服务质量(QoS)等一般网络策略。攻击者可以通过分析来自一个网络设备的规则被推入网络的条件以及规则的类型，推断出关于网络配置的敏感信息。*

*在探测阶段，攻击者试图在特定交换机上触发流量规则的安装。探测流量的具体特征取决于黑客想要接收的信息。*

*在下一阶段，攻击者将分析探测阶段生成的探测流量与安装的相应流量规则之间的相关性。他或她可以从该分析中推断出针对特定类型的网络流实施了什么网络策略。例如，如果攻击者在探测阶段使用网络扫描工具，他或她就可以发现防御策略是通过过滤网络流量来实现的。手动工作可能需要数周来收集数据，并且仍然需要具有预配置参数的算法，例如，需要多少特定分组来做出决定，因为数量取决于各种因素。在机器学习的帮助下，黑客可以自动完成这一过程。*

*通常，所有需要大量时间的信息收集任务也可以自动化。举个例子，*

*[DirBuster](https://sourceforge.net/projects/dirbuster/) ，一个用于[扫描](https://www.peerlyst.com/tags/scanning)可用目录和文件的工具，可以通过添加一种遗传算法，LSTMs 或 GANs 来改进，以生成与现有目录更相似的目录名。*

# *ML 用于收集离线用户的信息*

*如果网络犯罪活动涉及任何身体活动，如进入受保护的建筑物，那么网络攻击者最好能够跟踪保安人员。他们足够幸运，因为现在有了解决办法。*

*研究人员发现了一种在医院或家中监测患者生命体征的方法，无需可穿戴设备或笨重的哔哔声设备。更重要的是，这种方法可以用来看穿墙壁。在激动人心的 TED [演讲](https://www.ted.com/talks/dina_katabi_a_new_way_to_monitor_vital_signs_that_can_see_through_walls)中，他们展示了这个系统。*

*它捕捉无线信号(如 Wi-Fi)从人体反射回来的反射，为医护人员和患者创建可靠的生命体征记录。它给出了详细的跟踪数据，不仅显示了人是睡着还是醒着，还显示了睡眠的一个阶段。像大多数伟大的发明一样，这种设备也可以用于恶意的目的。想象一下，网络罪犯如何能够使用这种设备来检查安全警卫。*

*![](img/7d97b1a44c9aa59d342b101055f1b4cf.png)*

# *ML 用于收集关于离线资产的信息*

*当想到离线收集有关 IT 资产的信息时，首先想到的是在建筑物内找到摄像机和其他检测设备。所有这些设备都会产生信号，如果我们用这些符号的例子训练某种算法，就有可能检测到它们。*

# *保护*

*如何保护自己不成为受害者？不言而喻，您的个人信息不得公开。所以不要在社交网络上发布太多关于你自己的信息。这是一件很琐碎但很重要的事情。至于人身攻击，不幸的是，measuresю.没有保护措施目前，攻击的类型只是理论上的。*

# *模仿机器学习*

*冒充允许网络罪犯根据通信渠道和需要以不同的方式攻击受害者。攻击者能够在发送电子邮件或使用社交工程后，说服受害者点击带有漏洞或恶意软件的链接。因此，即使是打个电话也被认为是一种冒充的手段。假冒分为 3 种类型的网络活动:垃圾邮件，网络钓鱼和欺骗。*

# *垃圾邮件中的机器学习假冒*

*垃圾邮件是机器学习用于网络安全服务的最古老的领域之一。然而，这可能是最先涉及到 ML 传播网络攻击的领域之一。网络罪犯可以训练一个神经网络来创建垃圾邮件，而不是手动生成垃圾邮件，这不会引起怀疑。*

*然而，在处理电子邮件垃圾邮件时，很难模仿用户。如果你在电子邮件中代表公司的管理员要求员工更改密码或下载更新，你可能无法以完全相同的方式书写。除非你看到这位管理员写的一堆邮件，否则你无法复制这种风格。至于今天越来越受欢迎的信使，模仿人类甚至更容易。*

# *网络钓鱼中用于冒充的机器学习*

*与电子邮件网络钓鱼相比，社交媒体网络钓鱼的最大优势是公开性或容易获取个人信息。你可以通过阅读用户的帖子来监控和了解用户的行为。这一想法在最新的研究“[将数据科学武器化用于社会工程自动化 Twitter 上的 E2E 鱼叉式网络钓鱼](https://www.blackhat.com/docs/us-16/materials/us-16-Seymour-Tully-Weaponizing-Data-Science-For-Social-Engineering-Automated-E2E-Spear-Phishing-On-Twitter.pdf) —自动化[e2e](https://www.peerlyst.com/tags/e2e)T4Twitter 上的鱼叉式网络钓鱼中得到证明，该研究提出了 [SNAP_R](https://github.com/zerofox-oss/SNAP_R) ，这是一种显著增加网络钓鱼活动的自动化工具。而传统的自动网络钓鱼的准确率为 5%-14%，手动鱼叉式网络钓鱼的准确率为 45%。该方法的准确率在 30%左右，在某些情况下高达 66%，与自动化方法一样。研究人员使用马尔可夫模型根据用户以前的推文生成推文，并将结果与递归神经网络进行比较，特别是 LSTM。LSTM 氏症提供了更高的准确性，但需要更多的时间进行训练。*

*![](img/e4381a00327188034951ae0602f8ddcc.png)*

# *欺骗中的机器学习模仿*

*在人工智能的新时代，公司不仅可以创建假文本，还可以创建假声音或视频。专门从事媒体和视频模仿语音的初创公司 Lyrebird 展示了他们可以制造一个和你说话一模一样的机器人。随着数据量的增长和网络的发展，黑客可以展示更好的结果。我们不知道 Lyrebird 是如何工作的，黑客可能无法根据自己的需要使用这项服务，但他们可以发现更多的开放平台，如谷歌的 [WaveNet](https://deepmind.com/blog/wavenet-generative-model-raw-audio/) ，它们也能做到这一点。他们应用生成性对抗网络(GANs)。*

*照片也可以伪造。最近 Nvidia 的一篇论文介绍了一个工具，可以生成高质量的名人图片。*

*![](img/e85a0ce3552fbeae0e85805603a36626.png)*

*就在几年前，神经网络生成的视频和图像质量很差，只对研究文章有用。现在，几乎每个人都可以制作一个假视频，上面有名人或世界知名的政治家说他们从未说过的话或做他们从未做过的事(例如，你不会相信奥巴马在这个视频中说了什么)。它可以在公开可用的工具的帮助下实现，如 [DeepFake](https://www.kdnuggets.com/2018/03/exploring-deepfakes.html) 。*

*假货无处不在，这个问题越来越严重。下一步是什么？假公司？我们已经看过《T4》的第五集了。一个家伙用猫途鹰的假评论创建了一个假餐馆。手动操作并不容易，但人工智能可以帮助生成假账户。你所需要的只是训练人工智能，以便自动创建虚假资产和公司。想象一下，假城市及其新闻机构使用人工智能来创建新闻挂钩，以维持这个或那个议程。*

# *保护*

*虽然听起来有争议，但假货是真正的问题。幸运的是，有一些有前途的举措。[国防部展示了第一个工具，它能够检测深度伪造](https://www.technologyreview.com/s/611726/the-defense-department-has-produced-the-first-tools-for-catching-deepfakes/)。有个有趣的特点——假视频里人脸不眨眼。*

*AI 基金会在这一领域采取了另一项举措。这个名为 [Reality Defender](http://www.aifoundation.com/responsibility) 的项目旨在通过使用一个浏览器插件来保护用户免受假新闻的侵害。*

*至于网络钓鱼，对于社交媒体账户中的网络钓鱼，最可行的建议是检查并记录通过其他渠道和信使发送可疑消息的用户。他们的几个账户同时受损的可能性很小。*

# *针对未授权访问的机器学习*

*获得未经授权的访问是一个广泛的话题，但机器学习至少可以在两个最常见的领域发挥作用。这些是验证码旁路和密码暴力。*

# *验证码旁路的机器学习*

*模拟之后的下一个阶段是获取对用户帐户的未授权访问。*

*如果网络罪犯需要获得对用户会话的未授权访问，显而易见的方法是破坏帐户。对于大规模黑客攻击来说，令人讨厌的事情之一就是绕过验证码。许多计算机程序可以解决简单的验证码测试，但最复杂的部分是对象分割。*

*有许多研究论文描述了验证码旁路方法。2012 年 6 月 27 日，Claudia Cruz、Fernando Uceda 和 Leobardo Reyes 发表了机器学习的第一个例子。他们使用[支持向量机(SVM)方法](https://link.springer.com/chapter/10.1007/978-3-642-31149-9_16)破解了运行在 reCAPTCHA 图像上的系统，准确率达到 82%。所有的验证码机制都得到了显著的改进。然而，随后出现了一波论文，他们利用深度学习方法破解 CAPTCHA。*

*2016 年，发表了一篇[文章](https://deepmlblog.wordpress.com/2016/01/03/how-to-break-a-captcha-system/)，详细介绍了如何使用深度学习以 92%的准确率破解 simple-captcha。*

*![](img/6de55dc9bf0fabaf1b6cc35fcc7b35cd.png)*

*另一项[研究](https://github.com/arunpatala/captcha.irctc)使用了图像识别的最新进展之一——具有 34 层的深度残差网络来破解印度流行网站 IRCTC 的[验证码](https://www.peerlyst.com/tags/captcha)，准确率也达到 95–98%。这些文章大多采用基于字符的验证码。*

*一篇最鼓舞人心的论文在黑帽会议上发表。该研究论文名为“我是机器人”。他们曾经破解过最新的语义图像验证码，比较过各种机器学习算法。该论文承诺破解谷歌 reCAPTCHA 的准确率为 98%。*

*更糟糕的是，一篇新文章[指出，科学家警告即将出现的 100%验证码旁路方法。](https://www.npr.org/sections/thetwo-way/2017/10/26/560082659/ai-model-fundamentally-cracks-captchas-scientists-say)*

# *针对密码暴力的机器学习*

*网络犯罪分子可能在机器学习的帮助下发现优势的另一个领域是密码暴力。*

*马尔可夫模型在 2005 年首次被用于生成密码“猜测”，远在深度学习成为热门话题之前。如果你熟悉当前的神经网络和 LSTM，你可能听说过基于训练文本生成文本的网络。如果你给网络一个莎士比亚的作品，它会基于它创建一个新的文本，新生成的文本看起来就像是莎士比亚写的。同样的想法也可以用于生成密码。如果你可以用最常见的密码训练一个网络，它就会产生很多类似的密码。研究人员采用了这种方法，[将](https://courses.csail.mit.edu/6.857/2017/project/13.pdf)应用于密码，并收到了积极的结果，这比传统的突变更好地创建了密码列表，如将字母改为符号，例如从“s”改为“$”。*

*另一种方法在论文“ [PassGAN:密码猜测的深度学习方法](https://arxiv.org/pdf/1709.00440.pdf)中提到，研究人员使用 GAN 来生成密码。gan 是由两个网络组成的特殊类型的神经网络。一个通常被称为生成性的，另一个是歧视性的。一个是生成对立的例子，另一个是[测试](https://www.peerlyst.com/tags/testing)这个例子是否真实。其核心思想是训练基于真实密码数据的网络，这些数据来自最近的数据泄露事件。在公布了由 14 亿密码组成的最大数据库[之后，这个想法看起来对网络罪犯很有希望。](https://medium.com/4iqdelvedeep/1-4-billion-clear-text-credentials-discovered-in-a-single-database-3131d0a1ae14)*

# *保护*

*你如何保护自己？物体识别验证码已经死了。如果你为你的网站选择一个验证码，最好试试 MathCaptcha 或者它的替代品。其次，使用复杂的密码，排除简单的。避免数据库中的那些。唯一安全的随机密码是那些建立在短句基础上并混合了特殊字符的密码，或者是保存在密码管理工具中的完全随机的字符串。*

# *针对攻击的机器学习*

*网络罪犯想要使用机器学习的下一个领域是攻击本身。总的来说，有 3 个目标:间谍，破坏和欺诈。大多数情况下，它们都是通过恶意软件、间谍软件、勒索软件或任何其他类型的恶意程序来执行的，用户会因网络钓鱼而下载这些程序。攻击者也因为漏洞而上传。除了 DoS 攻击，还有一些不太常见的攻击，比如 crowdturfing。这些攻击比传统攻击更能从 ML 中获益。*

# *用于漏洞发现的机器学习*

*最常见的漏洞发现方法之一是模糊化。这意味着在应用程序中放入一个随机输入，并监视它是否会崩溃。有 2 个步骤需要自动化和人工智能的帮助。首先是实例的生成。通常如果你拿一个 PDF 文档，研究人员会通过随机改变一些字段来编辑这个文档。使用更智能的方法来产生突变，可以大大加快寻找会使应用程序崩溃的新文档示例的过程。*

*也可以实现类似 AlphaGo 使用的强化学习方法。如果 AlphaGO 模型在游戏中发现了故障，它也可以帮助发现安全问题。漏洞发现之后是崩溃分析。每一项分析都需要大量的人工工作。如果有可能训练一个模型来选择更相关的崩溃，将会节省时间和精力。此外，它使漏洞发现的成本大大降低。*

*[**在这里你可以找到更多关于机器学习的模糊化**](https://arxiv.org/abs/1701.07232)*

# *针对恶意软件/间谍软件/勒索软件的机器学习*

*用于恶意软件保护的机器学习可能是网络安全领域第一个商业上成功的 ML 实现。有几十篇科学论文描述了如何利用人工智能(AI)检测恶意软件[的不同技术。](/machine-learning-for-cybersecurity-101-7822b802790b)*

*网络罪犯如何部署机器学习来创建恶意软件？人们可以尝试使用强化学习。网络罪犯可以获取恶意软件示例，对其进行更改，发送到 VirusTotal，检查结果，进行其他更改，等等。*

*或者，面部识别可用于执行有针对性的攻击。DeepLocker 是恶意软件的一个例子，它隐藏自己，直到特定事件发生，例如，识别系统检测到目标人脸。*

# *拒绝服务攻击的机器学习*

*检测 DDoS 攻击最常用的方法是什么？在实施这种攻击的网络数据包中寻找常见模式。DDoS 防护总是像一场猫捉老鼠的游戏。攻击者试图通过伪造每个字段来使 DDoS 数据包与众不同，而防御者试图在欺骗的请求中找出共同的模式。在 AI 的帮助下，攻击者可以生成非常接近真实用户动作的 DDoS 数据包。它们可以嗅探正常流量，然后训练神经网络(如 GAN)发送合法数据包。在 DDoS 攻击中使用 AI 可以给这个领域带来显著的改变。*

# *面向人群漫游的机器学习*

*大众追随，产生包括假新闻在内的假信息。在机器学习的帮助下，网络犯罪分子可以降低这些攻击的成本，并使其自动化。*

*在 2017 年 9 月发表的[“在线评论系统中的自动众筹攻击和防御”](https://arxiv.org/pdf/1708.08151.pdf)研究中，介绍了该系统在 Yelp 上生成虚假评论的例子。优势不仅仅是无法检测到的 5 星评论，而是比人类写的评论得分更高的评论。*

*简单来说，众筹就是对众包服务的恶意使用。例如，攻击者为竞争对手的负面在线评论付费。这些评论经常未被发现，因为是真人写的，自动化工具在寻找软件攻击者。*

*假新闻只是众筹的一个例子。Max Tagmark 的书《[生活 3.0](https://www.amazon.com/Life-3-0-Being-Artificial-Intelligence/dp/1101946598) 》提到了另一个例子。有一个虚构的故事，一组黑客创造了人工智能，它能够在亚马逊土耳其机器人执行简单的工作任务。最重要的是，在亚马逊网络服务上购买这种人工智能硬件的成本比它在亚马逊 Mturk 上赚的钱要少。他们用了很短的时间就几乎让亚马逊破产了。*

# *用于网络犯罪自动化的机器学习*

*有经验的黑客可以使用机器学习来自动化各个领域的任务。几乎不可能预测什么时候和什么东西会被自动化，但是要知道网络犯罪组织有数百名成员，这需要不同类型的软件，如支持门户或支持机器人。*

*至于具体的网络犯罪任务，有一个新术语——[Hivenet](https://diginomica.com/2017/12/08/ai-machine-learning-cyber-crime-unholy-trinity/)——代表智能僵尸网络。这个想法是，如果网络罪犯手动管理僵尸网络，艾滋病毒可以有一种大脑来达到特定的事件，并根据它们改变行为。多个[机器人](https://www.peerlyst.com/tags/bots)将坐在设备中，并根据任务决定谁将使用受害者的资源。这就像是生活在有机体中的一系列寄生虫。*

***结论***

*上面的想法只是黑客可以使用机器学习的一些例子。*

*除了使用更安全的密码和在跟踪第三方网站时更加小心之外，我只能建议关注基于 ML 的安全系统，以便领先于犯罪者。*

*一两年前，每个人都对机器学习的使用持怀疑态度。今天的研究发现和它在产品中的实现证明了 ML 实际上是有效的，并且它会一直存在下去。否则，黑客将开始向前看，并从 ML 中受益。*

*如果你喜欢我的文章，请鼓掌，并订阅以了解更多关于机器学习和网络安全的不同方面。干杯。*