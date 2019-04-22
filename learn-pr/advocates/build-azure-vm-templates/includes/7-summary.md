<span data-ttu-id="0f671-101">在此模块中, 定义了 Azure 资源管理器的含义以及资源管理器模板中的内容。</span><span class="sxs-lookup"><span data-stu-id="0f671-101">In this module, you defined what Azure Resource Manager means and what's in a Resource Manager template.</span></span>

<span data-ttu-id="0f671-102">资源管理器模板是_声明性_的, 这__ 意味着您可以定义所需的资源, 并让资源管理器处理部署详细信息。</span><span class="sxs-lookup"><span data-stu-id="0f671-102">Resource Manager templates are _declarative_, meaning that you define _what_ resources you need and let Resource Manager handle the deployment details.</span></span>

<span data-ttu-id="0f671-103">您使用现有的 Azure 快速入门模板来部署 VM。</span><span class="sxs-lookup"><span data-stu-id="0f671-103">You used an existing Azure Quickstart template to deploy a VM.</span></span> <span data-ttu-id="0f671-104">快速入门模板是快速启动部署的绝佳方式。</span><span class="sxs-lookup"><span data-stu-id="0f671-104">Quickstart templates are a great way to jump-start your deployments.</span></span> <span data-ttu-id="0f671-105">它们还演示了您在创作自己的模板时可以学习的建议做法。</span><span class="sxs-lookup"><span data-stu-id="0f671-105">They also demonstrate recommended practices you can learn from as you author your own templates.</span></span>

<span data-ttu-id="0f671-106">此外, 还扩展了快速入门模板以在 VM 上配置 web 服务器软件。</span><span class="sxs-lookup"><span data-stu-id="0f671-106">You also extended your Quickstart template to configure web server software on your VM.</span></span> <span data-ttu-id="0f671-107">扩展现有模板是快速运行和了解这些组件如何组合在一起的一种极好的方法。</span><span class="sxs-lookup"><span data-stu-id="0f671-107">Extending an existing template is a great way to get something running quickly and understand how the pieces fit together.</span></span>

<span data-ttu-id="0f671-108">资源管理器模板也是可_组合_的。</span><span class="sxs-lookup"><span data-stu-id="0f671-108">Resource Manager templates are also _composable_.</span></span> <span data-ttu-id="0f671-109">在构建部署时, 可以编写较小的模板, 每个模板都可以定义系统的一部分, 然后将它们组合在一起, 以创建一个完整的系统。</span><span class="sxs-lookup"><span data-stu-id="0f671-109">As you build out your deployments, you can write smaller templates that each define a piece of the system and then combine them to create a complete system.</span></span>

<span data-ttu-id="0f671-110">考虑你在金融服务公司支持的分析师。</span><span class="sxs-lookup"><span data-stu-id="0f671-110">Think about the analysts you support at your financial services company.</span></span> <span data-ttu-id="0f671-111">在构建资源管理器模板库时, 您将能够更快地为每个分析者组合部署。</span><span class="sxs-lookup"><span data-stu-id="0f671-111">As you build your library of Resource Manager templates, you'll be able to assemble deployments for each analyst much more quickly.</span></span> <span data-ttu-id="0f671-112">在每个财务模型完成后, 只需运行一个 Azure CLI 命令即可销毁部署。</span><span class="sxs-lookup"><span data-stu-id="0f671-112">After each financial model completes, you need to run only a single Azure CLI command to tear down the deployment.</span></span>

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="learn-more"></a><span data-ttu-id="0f671-113">了解更多信息</span><span class="sxs-lookup"><span data-stu-id="0f671-113">Learn more</span></span>

<span data-ttu-id="0f671-114">要了解的一种很好的方法是这样做。</span><span class="sxs-lookup"><span data-stu-id="0f671-114">A great way to learn is by doing.</span></span> <span data-ttu-id="0f671-115">尝试编写可自动执行其中一个部署的资源管理器模板。</span><span class="sxs-lookup"><span data-stu-id="0f671-115">Try writing a Resource Manager template that automates one of your deployments.</span></span>

<span data-ttu-id="0f671-116">请参阅[Azure 文档中的资源管理器](https://docs.microsoft.com/azure/azure-resource-manager?azure-portal=true), 了解有关如何创建、部署、管理、审核和疑难解答模板的详细信息。</span><span class="sxs-lookup"><span data-stu-id="0f671-116">Refer to the [Resource Manager on Azure documentation](https://docs.microsoft.com/azure/azure-resource-manager?azure-portal=true) to learn more about how to create, deploy, manage, audit, and troubleshoot your templates.</span></span>

<span data-ttu-id="0f671-117">下面是一些资源, 这些资源更详细地介绍了本模块中所学的内容。</span><span class="sxs-lookup"><span data-stu-id="0f671-117">Here are some resources that go into more detail on what you learned in this module.</span></span>

* [<span data-ttu-id="0f671-118">Azure 快速入门模板</span><span class="sxs-lookup"><span data-stu-id="0f671-118">Azure Quickstart Templates</span></span>](https://azure.microsoft.com/resources/templates?azure-portal=true)
* [<span data-ttu-id="0f671-119">Azure 资源管理器可视化工具</span><span class="sxs-lookup"><span data-stu-id="0f671-119">Azure Resource Manager Visualizer</span></span>](http://armviz.io?azure-portal=true)
* [<span data-ttu-id="0f671-120">部署简单的 Windows VM</span><span class="sxs-lookup"><span data-stu-id="0f671-120">Deploy a simple Windows VM</span></span>](https://azure.microsoft.com/resources/templates/101-vm-simple-windows?azure-portal=true)
* [<span data-ttu-id="0f671-121">部署简单的 Ubuntu Linux 虚拟机</span><span class="sxs-lookup"><span data-stu-id="0f671-121">Deploy a simple Ubuntu Linux VM</span></span>](https://azure.microsoft.com/resources/templates/101-vm-simple-linux?azure-portal=true)

<span data-ttu-id="0f671-122">以下是我们在此处未讨论的一些主题, 但你可能会对你浏览和构建自己的模板感兴趣。</span><span class="sxs-lookup"><span data-stu-id="0f671-122">Here are some topics that we did not discuss here, but you might be interested in as you explore and build your own templates.</span></span>

* [<span data-ttu-id="0f671-123">使用 RBAC 和 Azure 资源管理器模板管理访问权限</span><span class="sxs-lookup"><span data-stu-id="0f671-123">Manage access using RBAC and Azure Resource Manager templates</span></span>](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-template?azure-portal=true)
* [<span data-ttu-id="0f671-124">在 Azure 资源管理器模板中使用条件</span><span class="sxs-lookup"><span data-stu-id="0f671-124">Use condition in Azure Resource Manager templates</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-tutorial-use-conditions?azure-portal=true)
* [<span data-ttu-id="0f671-125">在资源管理器模板部署中集成 Azure 密钥存储库</span><span class="sxs-lookup"><span data-stu-id="0f671-125">Integrate Azure Key Vault in Resource Manager Template deployment</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-tutorial-use-key-vault?azure-portal=true)
* [<span data-ttu-id="0f671-126">创建链接的 Azure 资源管理器模板</span><span class="sxs-lookup"><span data-stu-id="0f671-126">Create linked Azure Resource Manager templates</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-tutorial-create-linked-templates?azure-portal=true)
* [<span data-ttu-id="0f671-127">使用 Azure 资源管理器模板的最佳实践</span><span class="sxs-lookup"><span data-stu-id="0f671-127">Best Practices For Using Azure Resource Manager Templates</span></span>](https://blogs.msdn.microsoft.com/mvpawardprogram/2018/05/01/azure-resource-manager?azure-portal=true)
* [<span data-ttu-id="0f671-128">使用 azure 资源管理器解决常见的 azure 部署错误</span><span class="sxs-lookup"><span data-stu-id="0f671-128">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-common-deployment-errors?azure-portal=true)

