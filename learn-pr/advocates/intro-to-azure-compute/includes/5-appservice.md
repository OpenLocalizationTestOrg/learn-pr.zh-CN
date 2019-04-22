:::row:::
  :::column:::
    ![表示 Azure 应用服务的图像](../media/5-appservice.png)
  :::column-end:::
  :::column span="3":::
通过 Azure 应用服务, 您可以在您选择的编程语言中构建和托管 web 应用、后台作业、移动 backends 和 RESTful api, 而无需管理基础结构。 它提供自动缩放和高可用性, 支持 Windows 和 Linux, 并支持从 GitHub、Azure DevOps 或任何 Git 存储库进行自动部署, 以支持连续部署模型。
  :::column-end:::
:::row-end:::

此平台服务 (PaaS) 使你能够重点关注网站和 API 逻辑, 而 Azure 负责运行和扩展你的 web 应用程序的基础结构。 

## <a name="app-service-costs"></a>应用服务成本

你可以根据你选择的应用服务计划处理请求时为你的应用使用的 Azure 计算资源付费。 App Service plan 确定对主机专用的硬件量, 例如, 是专用硬件还是共享硬件, 以及为其保留的内存量。 甚至可以使用一种_免费_的层来承载小型低流量网站。

## <a name="types-of-web-apps"></a>web 应用程序的类型

使用 Azure 应用服务, 您可以承载最常见的 web 应用程序样式, 包括:

- Web 应用程序
- API 应用
- webjob
- 移动应用

Azure 应用服务处理您在托管 web 应用程序中处理的大多数基础结构决策: 部署和管理集成到平台中, 可以保护终结点, 可以快速扩展网站, 以处理高流量负载, 以及内置负载平衡和流量管理器可提供高可用性。 所有这些应用程序样式都托管在相同的基础结构中, 并共享这些优点。 这使 App Service 成为承载面向 web 的应用程序的理想选择。

### <a name="web-apps"></a>Web 应用程序

应用服务包括使用 ASP.NET、ASP.NET Core、Java、Ruby、node.js、PHP 或 Python 对承载 web 应用程序的完全支持。 可以选择 Windows 或 Linux 作为主机操作系统。 

### <a name="api-apps"></a>API 应用

与承载网站非常相似, 您可以使用您选择的语言和框架构建基于 REST 的 Web api。 获取完全 Swagger 支持, 以及在 Azure Marketplace 中打包和发布 API 的功能。 可以从任何基于 HTTP (s) 的客户端使用生成的应用程序。

### <a name="web-jobs"></a>Web 作业

通过 webjob, 可以在与 web 应用、API 应用或移动应用程序相同的上下文中运行程序 (.exe、Java、PHP、Python 或 node.js) 或脚本 (.cmd、.bat、PowerShell 或 Bash)。 可以对它们进行安排, 或由触发器运行。 这通常用于将后台任务作为应用程序逻辑的一部分运行。

### <a name="mobile-apps"></a>移动应用

使用 Azure 应用服务的移动应用功能为 iOS 和 Android 应用程序快速构建后端。 只需在 Azure 门户中单击几次, 即可执行以下操作:

- 将移动应用数据存储在基于云的 SQL 数据库中
- 根据常见的社交提供程序 (如 MSA、Google、Twitter 和 Facebook) 对客户进行身份验证
- 发送推送通知
- 在 c # 或 node.js 中执行自定义后端逻辑

在移动应用程序端, 存在针对本机 iOS & Android、Xamarin 和响应本机应用程序的 SDK 支持。