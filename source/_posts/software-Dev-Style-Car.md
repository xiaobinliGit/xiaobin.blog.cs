---
title: 转：通过造汽车了解软件开发模式 ​​​
date: 2017-12-22 20:41:31
categories:
  - 技术日志
  - 项目管理
tags:
  -Agile
cover: 
---
### 摘要: AGILE·LEAN·SCRUM·KANBAN
<!--more-->
## 前言
最近在翻公众号的时候，从【程序员那些事】里看到这么一篇文章，很有意思，全文由一副漫画入手，通俗易懂的把瀑布，Agile, Scrum，Kanban, Lean等常见软件开发模式的特点一一列举出来，值得收藏，遂转之。

#### 转自作者：伯乐在线 - 艾凌风

1913 年，美利坚工业之神——亨利福特，发明了世界上第一条流水线，汽车工业从此进入了大规模生产的时代。丰田公司提出的丰田生产系统（Toyota Production System）又为汽车工业带来了很多先进的生产和管理理念。

先进的生产和管理理念是一个行业从小作坊走向规模化的必经之路，软件工业虽然诞生较晚，但是发展却非常迅速，这也同样得益于软件工业开发和管理理念的发展。这其中就从汽车工业吸收了很多成熟的理念。

下面，就让我们通过这张出自 Toggle 的漫画，来了解软件开发模式的变迁史。

## 总览
![1](/CSBLOG/images/agile/1.jpg)

这张图片从上向下，五个房间，分别是瀑布模型（waterfall），敏捷开发（agile），看板（KANBAN），SCRUM 和精益软件开发（lean）。

除了瀑布模型这间小屋和其他小屋有着明显的界限之外，其他几种模型就像一个四合院，有着不可分割的关系，这也恰好表明，瀑布模式和敏捷开发模式是软件工业先后经历的两个阶段，而 KANBAN，SCRUM 和 LEAN 则是敏捷运动的产物。

OK，客官里边请，让我们进第一个屋子看看。
<div align=center>![2](/CSBLOG/images/agile/2.jpg)</div>
所谓瀑布模型，就是说，软件开发是按照一定顺序展开的（传统线性生产流程 : Traditional,linear production flow）。就像汽车生产的流水线一样，每个部门各司其责，工作按照顺序展开，交付件单通道线性流动。你看这幅图，总体上就分为：需求 → 设计 → 制造 → 测试，四个阶段。
<div align=center>![3](/CSBLOG/images/agile/3.jpg)</div>
在这个系统中，客户被排除在生产系统之外（围墙是密闭不透明的），它们只能从需求的接口人那里向系统输入需求（Client places order）。正因如此，客户无法理解生产所需的费用以及为什么交付总是会延期，因此，也难免会闹出下面这样的笑话：
<div align=center>![4](/CSBLOG/images/agile/4.jpg)</div>
客户希望你造一辆汽车，却只愿意支付一辆自行车的开发成本。这确实是司空见惯的事情 :(
需求接纳后进入到设计阶段：
<div align=center>![5](/CSBLOG/images/agile/5.jpg)</div>
设计定型后，进入制造阶段：
<div align=center>![6](/CSBLOG/images/agile/6.jpg)</div>
在线性的生产系统中，或者说在瀑布开发模式中，需求和设计是不可以进行修改的。工人被安排在制造系统中一个个工位上，每个人仅负责一个部件的生产和装配，就像这位盘腿坐着的“I know HTML”大哥一样，HTML 开发者只需要负责 HTML 的开发而无需，也不应该关心软件的其他部分。
<div align=center>![7](/CSBLOG/images/agile/7.jpg)</div>
喂喂喂，这位老铁，不上班玩什么球啊？哎，您也别怪他，毕竟交付件（整车/软件）还没有完成开发，测试工作自然无法开展，当然得等着咯。这也是瀑布模型最大的弊端，下游工作的开展严格依赖于上游交付件的完成情况，这无疑是一种浪费，在争分夺秒的软件开发过程中，你能忍受这种浪费吗？
<div align=center>![8](/CSBLOG/images/agile/8.jpg)</div>

汽车完成生产和测试之后，一次性交付到客户手中，完成客户的全部需求

### 走进新时代——敏捷开发模式

<div align=center>![9](/CSBLOG/images/agile/9.jpg)</div>
敏捷开发以用户的需求进化为核心，采用迭代、循序渐进的方法进行软件开发。在敏捷开发中，软件项目在构建初期被切分成多个子项目，各个子项目的成果都经过测试，具备可视、可集成和可运行使用的特征。换言之，就是把一个大项目分为多个相互联系，但也可独立运行的小项目，并分别完成，在此过程中软件一直处于可使用状态
有点书面是吧，其实很简单，敏捷开发的一个前提假设是：用户不可能在产品开发之前，设计之初就完整、明确的提出需求。期望用户在开发过程中不变更需求是不现实的。用户在开发前提出的需求，可能并不是它们最终希望得到的。下图可以显著说明这点：
<div align=center>![11](/CSBLOG/images/agile/11.jpg)</div>
<div align=center>![12](/CSBLOG/images/agile/12.jpg)</div>
在敏捷开发中，客户会参与到软件开发的整个流程中。整个开发过程不再是一堵不透风的墙，透明是关键（TRANSPARENCY IS KEY），但是，随着越来越多的用户参与进来，越来越多的问题也暴露出来了，越来越多不着调的需求也会被提出。
<div align=center>![13](/CSBLOG/images/agile/13.jpg)</div>

敏捷开发的另一个重要概念就是迭代，所谓迭代，就是不断对产品进行细微的、渐进式的改进（Small incremental changes）。

> “先给您上个小号的尾翼，用着好我再给您换个大的~” 

<div align=center>![14](/CSBLOG/images/agile/14.jpg)</div>
在敏捷开发中，生产不再是线性的，开发的同时还会进行测试工作，所有人都在同时工作。尴尬等待的日子一去不复返咯~
<div align=center>![15](/CSBLOG/images/agile/15.jpg)</div>

利用敏捷模式开发出的产品，相较于传统的软件交付方式，一个显著的特点是能够及时响应客户需求的变更，不断适应新的趋势。

<div align=center>![16](/CSBLOG/images/agile/16.jpg)</div>

这不，隔壁老王喜当爹了，之前定的法拉利显得有点不稳重，宝宝也没地方坐。我们的产品经理和开发人员快速响应，轿跑变商务也不是什么大问题~~ 当然，为谁辛苦为谁忙，客户爸爸们一定要买单呀！

> What?您问第一稿方案是什么样的？去翻垃圾桶吧！

<div align=center>![17](/CSBLOG/images/agile/17.jpg)</div>

### 一股来自东方的神秘力量——看板
<div align=center>![18](/CSBLOG/images/agile/18.jpg)</div>
相信各位也注意到了，相对于瀑布模式的井井有条，敏捷开发在灵活的同时，也带来了一定程度的混乱。就在这个节骨眼上，还得请这位来自东方的神秘人物——丰田看板大师（KANBAN SENSEI）给你点拨点拨。
<div align=center>![19](/CSBLOG/images/agile/19.jpg)</div>
KANBAN，不是汉语拼音，更不是英文缩写，它来自日语“看板”，カンバン的罗马拼写：Kanban。它正是丰田生产系统的一个重要概念：看板管理，常作“Kanban管理”，是丰田生产模式中的重要概念，指为了达到及时生产（JIT）方式控制现场生产流程的工具。及时生产方式中的拉式（Pull）生产系统可以使信息的流程缩短，并配合定量、固定装货容器等方式，而使生产过程中的物料流动顺畅。KANBAN要求把开发中的任务，以 TODO List 的方式表现出来：
<div align=center>![20](/CSBLOG/images/agile/20.jpg)</div>

形式可以是即时贴，也可以是可视化软件等等。在制造业中，看板也是非常重要的管理方法。也有将其称为目视化管理的。

### SCRUM 又是什么
<div align=center>![21](/CSBLOG/images/agile/21.jpg)</div>

> Scrum原始含义是指英式橄榄球次要犯规时在犯规地点对阵争球。争球双方各有8个队员参与，各方出3名前锋队员，并肩各站成一横排，面对面躬身互相顶肩，中间形成一条通道，其他队员分别站在后面，后排队员用肩顶住前锋队员的臀部，组成3、2、3或3、4、1阵形。然后，由犯规队的对方队员在对阵一侧1码外，用双手低手将球抛入通道，不得有利于本队。当球抛入通道时，前排的3对前锋队员互相抗挤，争相踢球给本方前卫或后卫队员，前卫和后卫队员必须等候前锋将球踢回后，方可移动

<div align=center>![22](/CSBLOG/images/agile/22.jpg)</div>

在敏捷开发领域，SCRUM是一种迭代式增量软件开发过程，它包括了一些预定义的角色：

* ##### 产品负责人 Product Owner

<div align=center>![23](/CSBLOG/images/agile/23.jpg) </div>

产品负责人负责维护订单
 
* ##### Scrum主管 Scrum Master

<div align=center>![24](/CSBLOG/images/agile/24.jpg) </div>

SCURM Master 对整个SCRUM 过程负责，不惜一切代价（AT ANY COST），保证团队的工作时间和计划。

* ##### 开发团队 Team

在 SCRUM 过程中，开发团队通常会进行冲刺 （Sprint），一个冲刺周期的长度通常是2-4周。
<div align=center>![25](/CSBLOG/images/agile/25.jpg)</div>
在这个冲刺过程中，开发小组专注于完成一组订单项的开发。比如：制造一个发动机
<div align=center>![26](/CSBLOG/images/agile/26.jpg)</div>
对于KANBAN 和 SCRUM，有人说 KANBAN vs SCRUM，也有人说 KANBAN+SCRUM，究竟谁是谁非，我看只有适合自己团队的才是最好的，毕竟方法和流程是为业务服务的。就这篇漫画来看，SCRUM + KANBAN 是两个避免混乱的好方法。
<div align=center>![27](/CSBLOG/images/agile/27.jpg)</div>

来来来，兄弟们，我们来开一个关于减少站会的站会~~
### 精益软件开发

<div align=center>![28](/CSBLOG/images/agile/28.jpg)</div>

第二次世界大战结束后，丰田公司前社长丰田英二曾经去美国汽车城底特律对福特生产线进行了考察，尽管福特高效的大规模生产线给他造成了很大的冲击，丰田英二还是非常理智的认识到了当时日本制造业所面临的困难。经济萧条，资源短缺，小批量差异化的需求使他不能盲目的引进这种大规模的生产方式，随后丰田公司发明并实践了一系列的管理和生产方法，这些方法在后来被统称为精益生产和管理方式（lean）<此处省略10万字，关于精益的理论阐述，有机会再唠>

精益生产的思想， 简单来说就是Just In Time（JIT），也就是说，只在必要的时候，按照需求的量，仅生产必要的产品，杜绝浪费。

<div align=center>![29](/CSBLOG/images/agile/29.jpg)</div>

> Eric Ries曾在《精益创业实战》中提出MVP（minimum viable product）概念，意即“最简可行产品”——用最快、最简明的方式建立一个可用的产品原型，这个原型要表达出你产品最终想要的效果，然后通过迭代来完善细节。

精益软件开发不再像传统的软件开发一样，耗时几年才向客户交付完整的软件。取而代之的是，优先建立一个最简可用的原型产品投放市场或交付到客户手中。
<div align=center>![30](/CSBLOG/images/agile/30.jpg)</div>
一辆最简可用的汽车是什么样子的呢？不就是四个轮子、一个方向盘、一个座椅然后一起装在底盘上么。能开、能停、能转弯不就是汽车嘛。让客户先享受到产品带来的收益是最重要的。

<div align=center>![31](/CSBLOG/images/agile/31.jpg)</div>

_BUT!!!_

你看，这里还有一位失落的大叔

<div align=center>![32](/CSBLOG/images/agile/32.jpg)</div>

尽管MPV 的概念听上去是如此的简单，可是实施起来却没有那么容易。

> 因为在设计产品原型的过程中，很多设计师是这么做的：把他们认为的产品应当具备的功能罗列出来，然后一一排除，排定优先级，决定哪个功能要在最初的版本中出现，而哪个可以靠后一些。但设计师们往往无法真的只把最必要的功能留在初级版本中——因为诱惑太多。设计师们总希望把很cool、很有惊喜的小细节带给用户来博取赞叹，但从全局来看，其实把某些功能刻意强加进产品，是会削弱产品整体流畅性的。Mr Jamie曾在其博客中把这种心理表现称作“艺术家心结”。

所有不必的东西（ALL NON-ESSENTIALS ARE THROWN OUT）都不能应用到当前的最小可用产品。你说，艺术家们得多伤心啊（愁的胡子都长一脸了）

此外，尽早交付产品给客户或部署到生产环境，也促进了 DevOps，持续集成（CI），生产环境测试（testing in production）等实践的发展。尽早交付产品，尽早从用户获取反馈，不论是好的还是坏的，促使问题尽早暴露，尽早修复，持续集成，持续改进。

<div align=center>![33](/CSBLOG/images/agile/33.jpg)</div>

### Reference:
1. http://blog.jobbole.com/113230/
2. https://toggl.com/developer-methods-infographic
3. Graphics support by my wife Yu Rongrong