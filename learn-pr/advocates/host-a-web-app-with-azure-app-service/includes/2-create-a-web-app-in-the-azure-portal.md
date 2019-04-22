在这里, 你将了解如何使用 azure 门户创建 azure 应用服务 web 应用。

## <a name="why-use-the-azure-portal"></a>为什么要使用 Azure 门户？

托管 web 应用程序的第一步是在 Azure 订阅中创建 web 应用程序 (应用服务应用程序)。

有几种方法可以创建 web 应用程序。 您可以使用 azure 门户、azure CLI、脚本或 IDE。

在这里, 我们将使用门户, 因为它是一个图形化体验, 它使其成为出色的学习工具。 门户可帮助您发现可用的功能、添加其他资源以及自定义现有资源。

## <a name="what-is-azure-app-service"></a>什么是 Azure 应用服务？

azure 应用服务是一个在 Azure 环境中针对承载 web 应用、REST api 和移动后端而优化的完全托管计算平台。

Microsoft Azure 提供的此平台即服务 (PaaS) 使你能够将重点放在 Azure 的构建面上, 而 Azure 负责运行和扩展应用程序的基础结构。

## <a name="how-to-create-a-web-app"></a>如何创建 web 应用程序

在需要托管您自己的应用程序时, 请访问 Azure 门户并创建**Web 应用程序**。 在 Azure 门户中创建**Web 应用程序**时, 实际上是在应用服务中创建一组托管资源, 您可以使用它来承载 Azure 支持的任何基于 Web 的应用程序, 无论它是 ASP.NET 核心、node.js、PHP, 等等。下图显示了配置应用程序使用的框架/语言的难易程度。

![用于配置 web 应用程序的应用程序设置的屏幕截图](../media/2-web-app-settings.png)

Azure 门户提供了用于创建 web 应用的模板。 此模板需要以下字段:

- **应用名称**: web 应用程序的名称。
- **订阅**: 有效且有效的订阅。
- **资源组**: 有效的资源组。 以下各节详细说明了资源组。
- **** 操作系统: 操作系统。 选项为: Windows、Linux 和 Docker 容器。 在 Windows 中, 可以托管各种技术中的任何类型的应用程序。 这同样适用于 linux 托管, 但在 linux 中, 任何 ASP.NET 应用程序都必须是 .net core framework 上的 ASP.Net Core。 最后一个选项是 Docker 容器, 您可以在其中直接将容器部署到由 Azure 托管和维护的容器中。 
- **App service plan/location**: 有效的 Azure 应用服务计划。 以下各节详细说明了应用服务计划是什么。
- **application insights**: 您可以打开 azure Application Insights 选项, 并受益于 azure 门户提供的监控和指标工具, 以帮助您跟踪应用程序的性能。

Azure 门户为你提供了通过多种可用工具管理、监视和控制 web 应用的最高的一手。

### <a name="deployment-slots"></a>部署槽

使用 Azure 门户, 可以轻松地将**部署槽**添加到应用服务 web 应用。 例如, 您可以创建一个**暂存**部署槽, 您可以在其中推送您的代码以在 Azure 上进行测试。 一旦您对代码感到满意, 就可以轻松地将暂存部署槽与生产槽**交换**。 在 Azure 门户中, 通过几个简单的鼠标单击即可完成所有这些操作。

![用于测试部署的暂存部署槽的屏幕截图](../media/2-deployment-slots.png)

### <a name="continuous-integrationdeployment-support"></a>持续集成/部署支持

azure 门户提供现成的持续集成和在开发计算机上使用 Azure DevOps、GitHub、Bitbucket、收存箱、OneDrive 或本地 Git 存储库进行部署。 使用上述任何源和应用服务连接 web 应用程序将通过自动同步代码以及将来在代码中对 web 应用程序所做的任何更改来为你执行其他操作。 此外, 使用 Azure DevOps, 您可以定义自己的生成和发布过程, 以编译源代码、运行测试、生成版本, 最后在每次提交代码时将发布部署到 web 应用中。 所有这些操作都隐式进行, 无需干预。

!["安装程序部署" 选项的屏幕截图, 并为部署源代码选择源](../media/2-continuous-integration.PNG)

### <a name="integrated-visual-studio-publishing-and-ftp-publishing"></a>集成的 Visual Studio 发布和 FTP 发布

除了能够为 web 应用程序设置持续集成/部署之外, 你还可以始终受益于与 Visual Studio 的紧密集成, 以通过 web Deploy 技术将 web 应用发布到 Azure。 此外, Azure 还支持 ftp, 但由于它缺少 Web Deploy 中的某些功能可供选择, 并且仅选择那些已更改或添加的文件, 并且不只是将所有内容发布到 Azure, 因此您更好的方法是使用 ftp 进行发布。

### <a name="built-in-auto-scale-support-automatic-scale-out-based-on-real-world-load"></a>内置自动缩放支持 (根据实际负载自动扩展)

Baked web app 中的功能是能够向上/向外扩展, 也可以向外扩展。根据 web 应用程序的使用情况, 您可以通过增加/降低承载 web 应用的基础计算机的资源来扩大应用范围。 资源可以是可用的核心数或可用 RAM 量。

另一方面, 横向扩展是增加运行 web 应用程序的计算机实例数量的能力。

## <a name="what-is-a-resource-group"></a>什么是资源组？

资源组是对给定应用程序和环境的相互依赖的资源和服务 (如虚拟机、web 应用、数据库等) 进行分组的一种方法。 将其视为一个**文件夹**, 用于将应用程序的元素分组。

资源组使您可以轻松地管理和删除资源。 它们还提供了一种方法, 用于监视、控制访问、设置和管理对运行应用程序所需的资源的集合以及客户端使用的资源的记帐。

## <a name="what-is-an-app-service-plan"></a>什么是应用服务计划？

App service plan 是一组可用于将应用服务应用程序部署到中的物理资源和容量。

Azure 门户提供了用于创建新的应用服务计划的模板。 此模板需要以下基本信息:

- 地区 (西 us、美国中部、北欧等)
- Scale count (一个、两个、三个实例等)
- 实例大小 (小、中或大)
- SKU 或定价层 (免费、共享、基本、Standard、Premium、PremiumV2 和独立)

azure 应用服务中托管的 Web 应用、移动应用和 API 应用程序以及 azure 函数均在应用服务计划中运行。 虽然您可以将不限数量的应用程序部署到应用服务计划中, 但您所使用的应用程序的数量也会很大, 具体取决于部署的应用程序的类型及其 CPU 使用率所需的资源。

你始终可以在 Azure 门户中使用应用服务计划来直观显示 CPU 和内存使用率, 以帮助确定将应用程序扩展或移动到另一个应用服务计划的需求。
