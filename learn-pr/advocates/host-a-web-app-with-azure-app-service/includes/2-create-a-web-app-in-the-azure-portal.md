<span data-ttu-id="95b10-101">在这里, 你将了解如何使用 azure 门户创建 azure 应用服务 web 应用。</span><span class="sxs-lookup"><span data-stu-id="95b10-101">Here, you'll learn how to create an Azure App Service web app using the Azure portal.</span></span>

## <a name="why-use-the-azure-portal"></a><span data-ttu-id="95b10-102">为什么要使用 Azure 门户？</span><span class="sxs-lookup"><span data-stu-id="95b10-102">Why use the Azure portal?</span></span>

<span data-ttu-id="95b10-103">托管 web 应用程序的第一步是在 Azure 订阅中创建 web 应用程序 (应用服务应用程序)。</span><span class="sxs-lookup"><span data-stu-id="95b10-103">The first step in hosting your web application is to create a web app (an App Service app) inside your Azure subscription.</span></span>

<span data-ttu-id="95b10-104">有几种方法可以创建 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="95b10-104">There are several ways you can create a web app.</span></span> <span data-ttu-id="95b10-105">您可以使用 azure 门户、azure CLI、脚本或 IDE。</span><span class="sxs-lookup"><span data-stu-id="95b10-105">You can use the Azure portal, the Azure CLI, a script, or an IDE.</span></span>

<span data-ttu-id="95b10-106">在这里, 我们将使用门户, 因为它是一个图形化体验, 它使其成为出色的学习工具。</span><span class="sxs-lookup"><span data-stu-id="95b10-106">Here, we are going to use the portal because it's a graphical experience, which makes it a great learning tool.</span></span> <span data-ttu-id="95b10-107">门户可帮助您发现可用的功能、添加其他资源以及自定义现有资源。</span><span class="sxs-lookup"><span data-stu-id="95b10-107">The portal helps you discover available features, add additional resources, and customize existing resources.</span></span>

## <a name="what-is-azure-app-service"></a><span data-ttu-id="95b10-108">什么是 Azure 应用服务？</span><span class="sxs-lookup"><span data-stu-id="95b10-108">What is Azure App Service?</span></span>

<span data-ttu-id="95b10-109">azure 应用服务是一个在 Azure 环境中针对承载 web 应用、REST api 和移动后端而优化的完全托管计算平台。</span><span class="sxs-lookup"><span data-stu-id="95b10-109">Azure App Service is a fully managed computing platform within the Azure environment that is optimized for hosting web apps, REST APIs, and mobile back ends.</span></span>

<span data-ttu-id="95b10-110">Microsoft Azure 提供的此平台即服务 (PaaS) 使你能够将重点放在 Azure 的构建面上, 而 Azure 负责运行和扩展应用程序的基础结构。</span><span class="sxs-lookup"><span data-stu-id="95b10-110">This platform as a service (PaaS) offered by Microsoft Azure allows you to focus on the build side of things while Azure takes care of the infrastructure to run and scale your applications.</span></span>

## <a name="how-to-create-a-web-app"></a><span data-ttu-id="95b10-111">如何创建 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="95b10-111">How to create a web app</span></span>

<span data-ttu-id="95b10-112">在需要托管您自己的应用程序时, 请访问 Azure 门户并创建**Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="95b10-112">When it's time to host your own app, you visit the Azure portal and create a **Web App**.</span></span> <span data-ttu-id="95b10-113">在 Azure 门户中创建**Web 应用程序**时, 实际上是在应用服务中创建一组托管资源, 您可以使用它来承载 Azure 支持的任何基于 Web 的应用程序, 无论它是 ASP.NET 核心、node.js、PHP, 等等。下图显示了配置应用程序使用的框架/语言的难易程度。</span><span class="sxs-lookup"><span data-stu-id="95b10-113">By creating a **Web App** in the Azure portal, you are actually creating a set of hosting resources in App Service, which you can use to host any web-based application that is supported by Azure, whether it be ASP.NET Core, Node.js, PHP, etc. The figure below shows how easy it is to configure the framework/language used by the app.</span></span>

![用于配置 web 应用程序的应用程序设置的屏幕截图](../media/2-web-app-settings.png)

<span data-ttu-id="95b10-115">Azure 门户提供了用于创建 web 应用的模板。</span><span class="sxs-lookup"><span data-stu-id="95b10-115">The Azure portal provides a template to create a web app.</span></span> <span data-ttu-id="95b10-116">此模板需要以下字段:</span><span class="sxs-lookup"><span data-stu-id="95b10-116">This template requires the following fields:</span></span>

- <span data-ttu-id="95b10-117">**应用名称**: web 应用程序的名称。</span><span class="sxs-lookup"><span data-stu-id="95b10-117">**App name**: The name of the web app.</span></span>
- <span data-ttu-id="95b10-118">**订阅**: 有效且有效的订阅。</span><span class="sxs-lookup"><span data-stu-id="95b10-118">**Subscription**: A valid and active subscription.</span></span>
- <span data-ttu-id="95b10-119">**资源组**: 有效的资源组。</span><span class="sxs-lookup"><span data-stu-id="95b10-119">**Resource group**: A valid resource group.</span></span> <span data-ttu-id="95b10-120">以下各节详细说明了资源组。</span><span class="sxs-lookup"><span data-stu-id="95b10-120">The sections below explain in detail what a resource group is.</span></span>
- <span data-ttu-id="95b10-121">\*\*\*\* 操作系统: 操作系统。</span><span class="sxs-lookup"><span data-stu-id="95b10-121">**OS**: The operating system.</span></span> <span data-ttu-id="95b10-122">选项为: Windows、Linux 和 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="95b10-122">The options are: Windows, Linux, and Docker containers.</span></span> <span data-ttu-id="95b10-123">在 Windows 中, 可以托管各种技术中的任何类型的应用程序。</span><span class="sxs-lookup"><span data-stu-id="95b10-123">On Windows, you can host any type of application from a variety of technologies.</span></span> <span data-ttu-id="95b10-124">这同样适用于 linux 托管, 但在 linux 中, 任何 ASP.NET 应用程序都必须是 .net core framework 上的 ASP.Net Core。</span><span class="sxs-lookup"><span data-stu-id="95b10-124">The same applies to Linux hosting, though on Linux, any ASP.NET apps must be ASP.Net Core on the .NET Core framework.</span></span> <span data-ttu-id="95b10-125">最后一个选项是 Docker 容器, 您可以在其中直接将容器部署到由 Azure 托管和维护的容器中。</span><span class="sxs-lookup"><span data-stu-id="95b10-125">The final option is Docker containers, where you can deploy your containers directly over containers hosted and maintained by Azure.</span></span> 
- <span data-ttu-id="95b10-126">**App service plan/location**: 有效的 Azure 应用服务计划。</span><span class="sxs-lookup"><span data-stu-id="95b10-126">**App Service plan/location**: A valid Azure App Service plan.</span></span> <span data-ttu-id="95b10-127">以下各节详细说明了应用服务计划是什么。</span><span class="sxs-lookup"><span data-stu-id="95b10-127">The sections below explain in detail what an App Service plan is.</span></span>
- <span data-ttu-id="95b10-128">**application insights**: 您可以打开 azure Application Insights 选项, 并受益于 azure 门户提供的监控和指标工具, 以帮助您跟踪应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="95b10-128">**Applications Insights**: You can turn on the Azure Application Insights option and benefit from the monitoring and metric tools that the Azure portal offers to help you keep an eye on the performance of your apps.</span></span>

<span data-ttu-id="95b10-129">Azure 门户为你提供了通过多种可用工具管理、监视和控制 web 应用的最高的一手。</span><span class="sxs-lookup"><span data-stu-id="95b10-129">The Azure portal gives you the upper hand in managing, monitoring, and controlling your web app through the many available tools.</span></span>

### <a name="deployment-slots"></a><span data-ttu-id="95b10-130">部署槽</span><span class="sxs-lookup"><span data-stu-id="95b10-130">Deployment slots</span></span>

<span data-ttu-id="95b10-131">使用 Azure 门户, 可以轻松地将**部署槽**添加到应用服务 web 应用。</span><span class="sxs-lookup"><span data-stu-id="95b10-131">Using the Azure portal, you can easily add **deployment slots** to an App Service web app.</span></span> <span data-ttu-id="95b10-132">例如, 您可以创建一个**暂存**部署槽, 您可以在其中推送您的代码以在 Azure 上进行测试。</span><span class="sxs-lookup"><span data-stu-id="95b10-132">For instance, you can create a **staging** deployment slot where you can push your code to test on Azure.</span></span> <span data-ttu-id="95b10-133">一旦您对代码感到满意, 就可以轻松地将暂存部署槽与生产槽**交换**。</span><span class="sxs-lookup"><span data-stu-id="95b10-133">Once you are happy with your code, you can easily **swap** the staging deployment slot with the production slot.</span></span> <span data-ttu-id="95b10-134">在 Azure 门户中, 通过几个简单的鼠标单击即可完成所有这些操作。</span><span class="sxs-lookup"><span data-stu-id="95b10-134">You do all this with a few simple mouse clicks in the Azure portal.</span></span>

![用于测试部署的暂存部署槽的屏幕截图](../media/2-deployment-slots.png)

### <a name="continuous-integrationdeployment-support"></a><span data-ttu-id="95b10-136">持续集成/部署支持</span><span class="sxs-lookup"><span data-stu-id="95b10-136">Continuous integration/deployment support</span></span>

<span data-ttu-id="95b10-137">azure 门户提供现成的持续集成和在开发计算机上使用 Azure DevOps、GitHub、Bitbucket、收存箱、OneDrive 或本地 Git 存储库进行部署。</span><span class="sxs-lookup"><span data-stu-id="95b10-137">The Azure portal provides out-of-the-box continuous integration and deployment with Azure DevOps, GitHub, Bitbucket, Dropbox, OneDrive, or a local Git repository on your development machine.</span></span> <span data-ttu-id="95b10-138">使用上述任何源和应用服务连接 web 应用程序将通过自动同步代码以及将来在代码中对 web 应用程序所做的任何更改来为你执行其他操作。</span><span class="sxs-lookup"><span data-stu-id="95b10-138">Connect your web app with any of the above sources and App Service will do the rest for you by auto-syncing code and any future changes on the code into the web app.</span></span> <span data-ttu-id="95b10-139">此外, 使用 Azure DevOps, 您可以定义自己的生成和发布过程, 以编译源代码、运行测试、生成版本, 最后在每次提交代码时将发布部署到 web 应用中。</span><span class="sxs-lookup"><span data-stu-id="95b10-139">Furthermore, with Azure DevOps, you can define your own build and release process that compiles your source code, runs the tests, builds a release, and finally deploys the release into your web app every time you commit the code.</span></span> <span data-ttu-id="95b10-140">所有这些操作都隐式进行, 无需干预。</span><span class="sxs-lookup"><span data-stu-id="95b10-140">All that happens implicitly without any need to intervene.</span></span>

!["安装程序部署" 选项的屏幕截图, 并为部署源代码选择源](../media/2-continuous-integration.PNG)

### <a name="integrated-visual-studio-publishing-and-ftp-publishing"></a><span data-ttu-id="95b10-142">集成的 Visual Studio 发布和 FTP 发布</span><span class="sxs-lookup"><span data-stu-id="95b10-142">Integrated Visual Studio publishing and FTP publishing</span></span>

<span data-ttu-id="95b10-143">除了能够为 web 应用程序设置持续集成/部署之外, 你还可以始终受益于与 Visual Studio 的紧密集成, 以通过 web Deploy 技术将 web 应用发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="95b10-143">In addition to being able to set up continuous integration/deployment for your web app, you can always benefit from the tight integration with Visual Studio to publish your web app to Azure via Web Deploy technology.</span></span> <span data-ttu-id="95b10-144">此外, Azure 还支持 ftp, 但由于它缺少 Web Deploy 中的某些功能可供选择, 并且仅选择那些已更改或添加的文件, 并且不只是将所有内容发布到 Azure, 因此您更好的方法是使用 ftp 进行发布。</span><span class="sxs-lookup"><span data-stu-id="95b10-144">Also, Azure supports FTP, although you are better off not using FTP for publishing because it lacks some capability in Web Deploy to pick and choose only those files that were changed or added, and not just publish everything to Azure!</span></span>

### <a name="built-in-auto-scale-support-automatic-scale-out-based-on-real-world-load"></a><span data-ttu-id="95b10-145">内置自动缩放支持 (根据实际负载自动扩展)</span><span class="sxs-lookup"><span data-stu-id="95b10-145">Built-in auto scale support (automatic scale-out based on real-world load)</span></span>

<span data-ttu-id="95b10-146">Baked web app 中的功能是能够向上/向外扩展, 也可以向外扩展。根据 web 应用程序的使用情况, 您可以通过增加/降低承载 web 应用的基础计算机的资源来扩大应用范围。</span><span class="sxs-lookup"><span data-stu-id="95b10-146">Baked into the web app is the ability to scale up/down or scale out. Depending on the usage of the web app, you can scale your app up/down by increasing/decreasing the resources of the underlying machine that is hosting your web app.</span></span> <span data-ttu-id="95b10-147">资源可以是可用的核心数或可用 RAM 量。</span><span class="sxs-lookup"><span data-stu-id="95b10-147">Resources can be number of cores or the amount of RAM available.</span></span>

<span data-ttu-id="95b10-148">另一方面, 横向扩展是增加运行 web 应用程序的计算机实例数量的能力。</span><span class="sxs-lookup"><span data-stu-id="95b10-148">Scaling out, on the other hand, is the ability to increase the number of machine instances that are running your web app.</span></span>

## <a name="what-is-a-resource-group"></a><span data-ttu-id="95b10-149">什么是资源组？</span><span class="sxs-lookup"><span data-stu-id="95b10-149">What is a resource group?</span></span>

<span data-ttu-id="95b10-150">资源组是对给定应用程序和环境的相互依赖的资源和服务 (如虚拟机、web 应用、数据库等) 进行分组的一种方法。</span><span class="sxs-lookup"><span data-stu-id="95b10-150">A resource group is a method of grouping interdependent resources and services such as virtual machines, web apps, databases, and more for a given application and environment.</span></span> <span data-ttu-id="95b10-151">将其视为一个**文件夹**, 用于将应用程序的元素分组。</span><span class="sxs-lookup"><span data-stu-id="95b10-151">Think of it as a **folder**, a place to group elements of your app.</span></span>

<span data-ttu-id="95b10-152">资源组使您可以轻松地管理和删除资源。</span><span class="sxs-lookup"><span data-stu-id="95b10-152">Resource groups allow you to easily manage and delete resources.</span></span> <span data-ttu-id="95b10-153">它们还提供了一种方法, 用于监视、控制访问、设置和管理对运行应用程序所需的资源的集合以及客户端使用的资源的记帐。</span><span class="sxs-lookup"><span data-stu-id="95b10-153">They also provide a way to monitor, control access, provision, and manage billing for collections of resources that are required to run an application or are used by a client.</span></span>

## <a name="what-is-an-app-service-plan"></a><span data-ttu-id="95b10-154">什么是应用服务计划？</span><span class="sxs-lookup"><span data-stu-id="95b10-154">What is an App Service plan?</span></span>

<span data-ttu-id="95b10-155">App service plan 是一组可用于将应用服务应用程序部署到中的物理资源和容量。</span><span class="sxs-lookup"><span data-stu-id="95b10-155">An App Service plan is a set of physical resources and capacity available to deploy your App Service apps into.</span></span>

<span data-ttu-id="95b10-156">Azure 门户提供了用于创建新的应用服务计划的模板。</span><span class="sxs-lookup"><span data-stu-id="95b10-156">The Azure portal provides a template to create a new App Service plan.</span></span> <span data-ttu-id="95b10-157">此模板需要以下基本信息:</span><span class="sxs-lookup"><span data-stu-id="95b10-157">This template requires the following basic information:</span></span>

- <span data-ttu-id="95b10-158">地区 (西 us、美国中部、北欧等)</span><span class="sxs-lookup"><span data-stu-id="95b10-158">Region (West US, Central US, North Europe, etc.)</span></span>
- <span data-ttu-id="95b10-159">Scale count (一个、两个、三个实例等)</span><span class="sxs-lookup"><span data-stu-id="95b10-159">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="95b10-160">实例大小 (小、中或大)</span><span class="sxs-lookup"><span data-stu-id="95b10-160">Instance size (Small, Medium, or Large)</span></span>
- <span data-ttu-id="95b10-161">SKU 或定价层 (免费、共享、基本、Standard、Premium、PremiumV2 和独立)</span><span class="sxs-lookup"><span data-stu-id="95b10-161">SKU, or pricing tier (Free, Shared, Basic, Standard, Premium, PremiumV2, and Isolated)</span></span>

<span data-ttu-id="95b10-162">azure 应用服务中托管的 Web 应用、移动应用和 API 应用程序以及 azure 函数均在应用服务计划中运行。</span><span class="sxs-lookup"><span data-stu-id="95b10-162">Web apps, mobile apps, and API apps hosted in Azure App Service, as well as Azure Functions, all run in an App Service plan.</span></span> <span data-ttu-id="95b10-163">虽然您可以将不限数量的应用程序部署到应用服务计划中, 但您所使用的应用程序的数量也会很大, 具体取决于部署的应用程序的类型及其 CPU 使用率所需的资源。</span><span class="sxs-lookup"><span data-stu-id="95b10-163">While you can deploy an unlimited number of applications into an App Service plan, the number you use greatly depends on the types of applications deployed and their required resources in CPU utilization.</span></span>

<span data-ttu-id="95b10-164">你始终可以在 Azure 门户中使用应用服务计划来直观显示 CPU 和内存使用率, 以帮助确定将应用程序扩展或移动到另一个应用服务计划的需求。</span><span class="sxs-lookup"><span data-stu-id="95b10-164">You can always use your App Service plan in the Azure portal to visualize your CPU and memory utilization to help determine your needs for scaling or moving applications into another App Service plan.</span></span>