:::row:::
  :::column:::
    ![表示 Azure 应用服务的图像](../media/5-appservice.png)
  :::column-end:::
  :::column span="3":::
<span data-ttu-id="e56fc-102">通过 Azure 应用服务, 您可以在您选择的编程语言中构建和托管 web 应用、后台作业、移动 backends 和 RESTful api, 而无需管理基础结构。</span><span class="sxs-lookup"><span data-stu-id="e56fc-102">Azure App Service enables you to build and host web apps, background jobs, mobile backends, and RESTful APIs in the programming language of your choice without managing infrastructure.</span></span> <span data-ttu-id="e56fc-103">它提供自动缩放和高可用性, 支持 Windows 和 Linux, 并支持从 GitHub、Azure DevOps 或任何 Git 存储库进行自动部署, 以支持连续部署模型。</span><span class="sxs-lookup"><span data-stu-id="e56fc-103">It offers auto-scaling and high availability, supports both Windows and Linux, and enables automated deployments from GitHub, Azure DevOps, or any Git repo to support a continuous deployment model.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="e56fc-104">此平台服务 (PaaS) 使你能够重点关注网站和 API 逻辑, 而 Azure 负责运行和扩展你的 web 应用程序的基础结构。</span><span class="sxs-lookup"><span data-stu-id="e56fc-104">This platform as a service (PaaS) allows you to focus on the website and API logic while Azure takes care of the infrastructure to run and scale your web applications.</span></span> 

## <a name="app-service-costs"></a><span data-ttu-id="e56fc-105">应用服务成本</span><span class="sxs-lookup"><span data-stu-id="e56fc-105">App Service costs</span></span>

<span data-ttu-id="e56fc-106">你可以根据你选择的应用服务计划处理请求时为你的应用使用的 Azure 计算资源付费。</span><span class="sxs-lookup"><span data-stu-id="e56fc-106">You pay for the Azure compute resources your app uses while it processes requests based on the App Service Plan you choose.</span></span> <span data-ttu-id="e56fc-107">App Service plan 确定对主机专用的硬件量, 例如, 是专用硬件还是共享硬件, 以及为其保留的内存量。</span><span class="sxs-lookup"><span data-stu-id="e56fc-107">The App Service plan determines how much hardware is devoted to your host - for example, whether it's dedicated or shared hardware, and how much memory is reserved for it.</span></span> <span data-ttu-id="e56fc-108">甚至可以使用一种_免费_的层来承载小型低流量网站。</span><span class="sxs-lookup"><span data-stu-id="e56fc-108">There is even a _free_ tier you can use to host small, low-traffic sites.</span></span>

## <a name="types-of-web-apps"></a><span data-ttu-id="e56fc-109">web 应用程序的类型</span><span class="sxs-lookup"><span data-stu-id="e56fc-109">Types of web apps</span></span>

<span data-ttu-id="e56fc-110">使用 Azure 应用服务, 您可以承载最常见的 web 应用程序样式, 包括:</span><span class="sxs-lookup"><span data-stu-id="e56fc-110">With Azure App Service, you can host most common web app styles including:</span></span>

- <span data-ttu-id="e56fc-111">Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="e56fc-111">Web Apps</span></span>
- <span data-ttu-id="e56fc-112">API 应用</span><span class="sxs-lookup"><span data-stu-id="e56fc-112">API Apps</span></span>
- <span data-ttu-id="e56fc-113">webjob</span><span class="sxs-lookup"><span data-stu-id="e56fc-113">WebJobs</span></span>
- <span data-ttu-id="e56fc-114">移动应用</span><span class="sxs-lookup"><span data-stu-id="e56fc-114">Mobile Apps</span></span>

<span data-ttu-id="e56fc-115">Azure 应用服务处理您在托管 web 应用程序中处理的大多数基础结构决策: 部署和管理集成到平台中, 可以保护终结点, 可以快速扩展网站, 以处理高流量负载, 以及内置负载平衡和流量管理器可提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="e56fc-115">Azure App Service handles most of the infrastructure decisions you deal with in hosting web apps: deployment and management are integrated into the platform, endpoints can be secured, sites can be scaled quickly to handle high traffic loads, and the built-in load balancing and traffic manager provide high availability.</span></span> <span data-ttu-id="e56fc-116">所有这些应用程序样式都托管在相同的基础结构中, 并共享这些优点。</span><span class="sxs-lookup"><span data-stu-id="e56fc-116">All of these app styles are hosted in the same infrastructure and share these benefits.</span></span> <span data-ttu-id="e56fc-117">这使 App Service 成为承载面向 web 的应用程序的理想选择。</span><span class="sxs-lookup"><span data-stu-id="e56fc-117">This makes App Service the ideal choice to host web-oriented applications.</span></span>

### <a name="web-apps"></a><span data-ttu-id="e56fc-118">Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="e56fc-118">Web Apps</span></span>

<span data-ttu-id="e56fc-119">应用服务包括使用 ASP.NET、ASP.NET Core、Java、Ruby、node.js、PHP 或 Python 对承载 web 应用程序的完全支持。</span><span class="sxs-lookup"><span data-stu-id="e56fc-119">App Service includes full support for hosting web apps using ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP, or Python.</span></span> <span data-ttu-id="e56fc-120">可以选择 Windows 或 Linux 作为主机操作系统。</span><span class="sxs-lookup"><span data-stu-id="e56fc-120">You can choose either Windows or Linux as the host operating system.</span></span> 

### <a name="api-apps"></a><span data-ttu-id="e56fc-121">API 应用</span><span class="sxs-lookup"><span data-stu-id="e56fc-121">API Apps</span></span>

<span data-ttu-id="e56fc-122">与承载网站非常相似, 您可以使用您选择的语言和框架构建基于 REST 的 Web api。</span><span class="sxs-lookup"><span data-stu-id="e56fc-122">Much like hosting a website, you can build REST-based Web APIs using your choice of language and framework.</span></span> <span data-ttu-id="e56fc-123">获取完全 Swagger 支持, 以及在 Azure Marketplace 中打包和发布 API 的功能。</span><span class="sxs-lookup"><span data-stu-id="e56fc-123">You get full Swagger support, and the ability to package and publish your API in the Azure Marketplace.</span></span> <span data-ttu-id="e56fc-124">可以从任何基于 HTTP (s) 的客户端使用生成的应用程序。</span><span class="sxs-lookup"><span data-stu-id="e56fc-124">The produced apps can be consumed from any HTTP(s) based client.</span></span>

### <a name="web-jobs"></a><span data-ttu-id="e56fc-125">Web 作业</span><span class="sxs-lookup"><span data-stu-id="e56fc-125">Web Jobs</span></span>

<span data-ttu-id="e56fc-126">通过 webjob, 可以在与 web 应用、API 应用或移动应用程序相同的上下文中运行程序 (.exe、Java、PHP、Python 或 node.js) 或脚本 (.cmd、.bat、PowerShell 或 Bash)。</span><span class="sxs-lookup"><span data-stu-id="e56fc-126">WebJobs allows you to run a program (.exe, Java, PHP, Python or Node.js) or script (.cmd, .bat, PowerShell, or Bash) in the same context as a web app, API app, or mobile app.</span></span> <span data-ttu-id="e56fc-127">可以对它们进行安排, 或由触发器运行。</span><span class="sxs-lookup"><span data-stu-id="e56fc-127">They can be scheduled, or run by a trigger.</span></span> <span data-ttu-id="e56fc-128">这通常用于将后台任务作为应用程序逻辑的一部分运行。</span><span class="sxs-lookup"><span data-stu-id="e56fc-128">This is often used to run background tasks as part of your application logic.</span></span>

### <a name="mobile-apps"></a><span data-ttu-id="e56fc-129">移动应用</span><span class="sxs-lookup"><span data-stu-id="e56fc-129">Mobile Apps</span></span>

<span data-ttu-id="e56fc-130">使用 Azure 应用服务的移动应用功能为 iOS 和 Android 应用程序快速构建后端。</span><span class="sxs-lookup"><span data-stu-id="e56fc-130">Use the Mobile Apps feature of Azure App Service to quickly build a back-end for iOS and Android apps.</span></span> <span data-ttu-id="e56fc-131">只需在 Azure 门户中单击几次, 即可执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="e56fc-131">With just a few clicks in the Azure portal you can:</span></span>

- <span data-ttu-id="e56fc-132">将移动应用数据存储在基于云的 SQL 数据库中</span><span class="sxs-lookup"><span data-stu-id="e56fc-132">Store mobile app data in a cloud-based SQL database</span></span>
- <span data-ttu-id="e56fc-133">根据常见的社交提供程序 (如 MSA、Google、Twitter 和 Facebook) 对客户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="e56fc-133">Authenticate customers against common social providers such as MSA, Google, Twitter and Facebook</span></span>
- <span data-ttu-id="e56fc-134">发送推送通知</span><span class="sxs-lookup"><span data-stu-id="e56fc-134">Send push notifications</span></span>
- <span data-ttu-id="e56fc-135">在 c # 或 node.js 中执行自定义后端逻辑</span><span class="sxs-lookup"><span data-stu-id="e56fc-135">Execute custom back-end logic in C# or Node.js</span></span>

<span data-ttu-id="e56fc-136">在移动应用程序端, 存在针对本机 iOS & Android、Xamarin 和响应本机应用程序的 SDK 支持。</span><span class="sxs-lookup"><span data-stu-id="e56fc-136">On the mobile app side, there is SDK support for native iOS & Android, Xamarin, and React native apps.</span></span>