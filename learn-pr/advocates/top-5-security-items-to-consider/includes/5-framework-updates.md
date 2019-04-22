许多开发人员考虑使用框架和库来构建其软件, 主要由功能或个人首选项决定。 但是, 您选择的框架是一项重要决定, 而不仅仅是从设计和功能角度进行, 也可以从_安全_角度进行。 选择具有新式安全功能的框架并将其保持最新状态是确保您的应用程序安全的最佳方式之一。

## <a name="choose-your-framework-carefully"></a>仔细选择框架

选择框架时, 有关安全性的最重要因素是它支持的程度。 最佳框架具有规定的安全排列, 并受大型社区 (改进和测试框架) 的支持。 任何软件都不是 100% 的缺陷, 也不是完全安全, 但如果发现了一个安全漏洞, 我们想要确保它将被关闭或具有快速提供的解决方法。

通常, "很受支持" 的意思是 "新式"。 较旧的框架通常要替换或最终渐隐为热门程度。 即使您对较旧框架的 (或多个应用程序) 具有极大的体验, 你也可以更好地选择具有所需功能的新式库。 新式框架通常在以前的迭代中学习的教训上构建, 这使为新应用程序选择它们的形式是威胁面降低的形式。 如果在旧版应用程序的旧框架中发现了漏洞, 你将需要考虑一个更多的应用程序。

若要详细了解如何安全设计和减少威胁图面, 请参阅[在 Azure 中设计安全性](../../design-for-security-in-azure/index.yml)。

## <a name="keep-your-framework-updated"></a>保持框架更新

软件开发框架 (如 Java 春季和 .net Core release 更新和新版本) 将定期更新。 这些更新包括新功能、旧功能的删除以及安全修补程序或改进。 当我们允许我们的框架过期时, 它会创建 "技术债务"。 我们获取的时间越早, 就越难和 riskier 将代码带到最新版本。 此外, 与最初的框架选择非常相似, 在旧版本的框架中保持较旧版本, 使您能够在更高版本的 framework 中修复更多安全威胁。

在 Apache Struts 框架中, 从2016-2017 到[30 个漏洞](https://www.cvedetails.com/product/6117/Apache-Struts.html?vendor_id=45)的示例。 开发团队快速解决这些问题, 但有些公司未应用修补程序并[以数据泄露的形式支付价格](https://www.zdnet.com/article/equifax-confirms-apache-struts-flaw-it-failed-to-patch-was-to-blame-for-data-breach/)。 **确保将您的框架和库保持最**新状态。

### <a name="how-do-i-update-my-framework"></a>如何更新我的框架？

某些框架 (如 Java 或 .net) 需要安装并倾向于在已知节奏上发布。 最好查看新版本, 并计划让代码的分支在发布时尝试使用它。 举例来说, .net Core 维护了一个[发布说明页面](https://github.com/dotnet/core/tree/master/release-notes), 您可以查看该页面以查找可用的最新版本。

更多专门化的库 (如 JavaScript 框架) 或 .net 组件可以通过程序包管理器进行更新。 **NPM**和**Webpack**是 web 项目的常用选项, 大多数 ide 或生成工具都支持这些选项。 在 .net 中, 我们使用**NuGet**管理组件依赖项。 与更新核心框架一样, 对代码进行分支、更新组件和测试是验证依赖项的新版本的一种很棒的技术。

> [!NOTE]
> 命令行工具有一个`add package`和选项可`remove package`用于添加或删除 NuGet 包, 但不具有相应`update package`的命令。 `dotnet` 但是, 它可以在您的项目`dotnet add package <package-name>`中运行, 它会自动将包_升级_到最新版本。 这是更新依赖项而无需打开 IDE 的简单方法。

## <a name="take-advantage-of-built-in-security"></a>充分利用内置安全性

请始终检查以了解您的框架提供了哪些安全功能。 如果有内置的标准技术或功能,**决不**要汇总自己的安全性。 此外, 依靠经验证的算法和工作流, 因为许多专家、critiqued 和强化都经常对这些算法和工作流进行了仔细审查, 因此您可以确信它们是可靠且安全的。

.net Core framework 具有无数个安全功能, 下面是文档中的几个核心起始位置。
* [身份验证-身份管理](https://docs.microsoft.com/aspnet/core/security/authentication/index?view=aspnetcore-2.1)
* [批准](https://docs.microsoft.com/aspnet/core/security/authorization/index?view=aspnetcore-2.1)
* [数据保护](https://docs.microsoft.com/aspnet/core/security/data-protection/index?view=aspnetcore-2.1)
* [安全配置](https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/index?view=aspnetcore-2.1)
* [安全扩展性 api](https://docs.microsoft.com/aspnet/core/security/data-protection/extensibility/index?view=aspnetcore-2.1)

这些功能中的每一项都是由专家在其字段中编写的, 然后 battered 使用测试来确保其按预期方式工作, 并且仅按预期工作。 其他框架提供了类似的功能-请与提供框架的供应商联系, 以找出它们在每个类别中所具有的功能。

> [!WARNING]
> 编写您自己的安全控件 (而不是使用框架提供的控件) 不仅浪费时间, 而且安全性较差。


## <a name="azure-security-center"></a>Azure 安全中心

使用 Azure 托管你的 web 应用程序时, 安全中心会在你的 framework 已过期时向你发出警告, 作为 "建议" 选项卡的一部分。 不要忘记在这里看, 看看是否有与你的应用有关的警告。

![Azure 安全中心推荐了框架升级。](../media/5-ASCFramework.png)


## <a name="summary"></a>摘要

只要有可能, 请选择一个新式框架来构建您的应用程序, 始终使用内置安全功能, 并确保使其保持最新。 这些简单的规则将有助于确保应用程序以坚实的基础启动。
