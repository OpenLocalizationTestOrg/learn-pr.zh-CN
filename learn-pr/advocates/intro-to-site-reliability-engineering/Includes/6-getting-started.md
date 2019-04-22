作为本模块中的最后一个单元, 我们将讨论从这里获取的位置 (如果您对浏览 SRE 感兴趣)。 

## <a name="reading-and-watching"></a>阅读和监视

有关 SRE 的更多详细信息, 最好的来源是已在主题中发布的书籍的 trio

1. [_网站可靠性工程: Google 如何运行生产系统_](http://shop.oreilly.com/product/0636920041528.do)(称为 "SRE Book")
1. [_网站可靠性工作簿: 实现 SRE 的实际方法_](http://shop.oreilly.com/product/0636920132448.do)(称为 "SRE 工作簿")
1. [_寻求 SRE: 有关在规模扩展时运行生产系统的对话_](http://shop.oreilly.com/product/0636920063964.do)

(作为简短的公开, 本模块的主要作者是第三本书的 curator/编辑器)

每本书都提供一组重要的信息:

- SRE 书籍-提供了 Google 在几年中实现 SRE 的方式的详细说明。

- sre 工作簿-提供了对在 Google 和其他几个位置提供更详细解释 (而不只是在 Google 上为 sre 的 "内容" 和 "原因" 和 "原因") 的 sre 工作簿。

- 寻求 sre-提供更广泛的 sre world 视图, 超出其来源, 包括有关它在其他环境中实现方式的信息。

务必阅读全部三本书, 并进行关键眼。 并非这些书籍中的所有内容都适用于您和您的组织。 需要一些时间来确定您确定的信息可以提供一些正值。 考虑您组织的文化和价值可以支持 SRE 工作 (如所述) 以及可能会导致更多挑战的部分。

如果你发现更多的视觉人, 请尝试通过在 SREcon14 会议上 Ben Treynor 来观看谈话[密钥](https://www.usenix.org/conference/srecon14/technical-sessions/presentation/keys-sre)。 Treynor 提供了真正 cogent 的解释, 即他认为 SRE (至少在 Google 上下文中)。 与[此会议系列](https://www.usenix.org/conferences/byname/925)中的 SRE 讨论的其他记录, 其他记录也可能非常有用。

## <a name="talk-to-other-interested-people"></a>与其他感兴趣的人交谈

与在 SRE 上阅读一样重要的是, 与您的同行讨论它通常也更重要。 若要了解对主题的细微了解, 请务必对 SRE 的成功和失败进行讨论。 

有许多 meetups 和会议的功能在 SRE 内容中。 或许最直接相关的是由 USENIX 加入的全球分布式[SREcon 会议](https://www.usenix.org/conferences/byname/925)(免责声明: 此模块的主要作者是 SREcon 的 cofounders 之一)。

越来越多的 SRE 内容将成为像[速度](https://conferences.oreilly.com/velocity)、 [LISA](https://www.usenix.org/conferences/byname/5)和本地 DevOps 会议这样的会议, 如[DevOps 天](https://www.devopsdays.org)。 在任何可以找到该主题的地方查找此内容和其他感兴趣的人。

## <a name="first-steps-at-work"></a>工作的首要步骤

如果您想要开始了解如何将 SRE 引入您的环境中, 请务必记住, SRE 不是 "全部或无" 主张。  您可以在小型步骤中开始采用 SRE 原则和做法。

Mikey Dickerson, 从他的工作, 在什么情况下将成为美国数字服务 (他们负责保存 healthcare.gov) 的一项良好的用户已建议在 homage 到 Maslow 的需求层次结构中实现可靠性的层次结构。 它在第一项 SRE 书籍的 "[实践" 部分](https://landing.google.com/sre/book/chapters/part3.html)中引用。

此层次结构建议一个必须首先在你的环境中获取监控, 并可信赖。 这也必须是对环境进行 SRE 的第一步。 如果您无法衡量它是否可靠 (或正在变得更糟), 则无法判断它是否可靠。

一旦拥有可信任的监视平台, 下一个可访问的步骤就是在工作中选取一个服务, 并开始与之相关的 SLI 和 SLO 对话。 简单开始。 为服务创建 SLIs 和 slo, 在您的监视系统中实施这些服务, 并查看使用 SRE lens 在可靠性方面开始引起的问题时, 会发生什么情况。 这是一个很好的开端。
