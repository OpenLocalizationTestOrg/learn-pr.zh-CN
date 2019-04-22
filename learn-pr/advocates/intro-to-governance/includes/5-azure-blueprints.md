<span data-ttu-id="a772b-101">遵守安全性或合规性要求 (无论是政府还是行业要求) 可能会非常困难且耗时。</span><span class="sxs-lookup"><span data-stu-id="a772b-101">Adhering to security or compliance requirements, whether government or industry requirements, can be difficult and time-consuming.</span></span> <span data-ttu-id="a772b-102">若要帮助您对部署进行审核、跟踪功能和合规性, 请使用**Azure 蓝图**项目和工具。</span><span class="sxs-lookup"><span data-stu-id="a772b-102">To help you with auditing, traceability, and compliance with your deployments, use **Azure Blueprint** artifacts and tools.</span></span> 

:::row:::
  :::column:::
    ![表示 Azure 蓝图的图标](../media/5-azureblueprint.png)
  :::column-end:::
    :::column span="3":::
<span data-ttu-id="a772b-104">通过**azure 蓝图**, 可以定义一组可重复的 Azure 资源, 以实现并遵守组织的标准、模式和要求。</span><span class="sxs-lookup"><span data-stu-id="a772b-104">**Azure Blueprint** allows you to define a repeatable set of Azure resources that implement and adhere to your organization's standards, patterns, and requirements.</span></span> <span data-ttu-id="a772b-105">蓝图使开发团队能够快速构建和部署新的环境, 并在组织合规性的基础上构建与一组可加快开发和交付的内置组件的知识。</span><span class="sxs-lookup"><span data-stu-id="a772b-105">Blueprint enables development teams to rapidly build and deploy new environments with the knowledge that they're building within organizational compliance with a set of built-in components that speed up development and delivery.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="a772b-106">Azure 蓝图是一种用于协调各种资源模板和其他项目的部署的声明性方法, 例如:</span><span class="sxs-lookup"><span data-stu-id="a772b-106">Azure Blueprint is a declarative way to orchestrate the deployment of various resource templates and other artifacts, such as:</span></span>

- <span data-ttu-id="a772b-107">角色分配</span><span class="sxs-lookup"><span data-stu-id="a772b-107">Role assignments</span></span>
- <span data-ttu-id="a772b-108">策略分配</span><span class="sxs-lookup"><span data-stu-id="a772b-108">Policy assignments</span></span>
- <span data-ttu-id="a772b-109">Azure 资源管理器模板</span><span class="sxs-lookup"><span data-stu-id="a772b-109">Azure Resource Manager templates</span></span>
- <span data-ttu-id="a772b-110">资源组</span><span class="sxs-lookup"><span data-stu-id="a772b-110">Resource groups</span></span>

<span data-ttu-id="a772b-111">实现 Azure 蓝图的过程包括以下高级步骤:</span><span class="sxs-lookup"><span data-stu-id="a772b-111">The process of implementing Azure Blueprint consists of the following high-level steps:</span></span>

1. <span data-ttu-id="a772b-112">创建 Azure 蓝图</span><span class="sxs-lookup"><span data-stu-id="a772b-112">Create an Azure Blueprint</span></span>
2. <span data-ttu-id="a772b-113">分配蓝图</span><span class="sxs-lookup"><span data-stu-id="a772b-113">Assign the blueprint</span></span>
3. <span data-ttu-id="a772b-114">跟踪蓝图分配</span><span class="sxs-lookup"><span data-stu-id="a772b-114">Track the blueprint assignments</span></span>

<span data-ttu-id="a772b-115">使用 Azure 蓝图, 将保留蓝图定义 (_应_部署的内容) 和蓝图分配 (部署的内容) __ 之间的关系。</span><span class="sxs-lookup"><span data-stu-id="a772b-115">With Azure Blueprint, the relationship between the blueprint definition (what _should be_ deployed) and the blueprint assignment (what _was_ deployed) is preserved.</span></span> <span data-ttu-id="a772b-116">此连接支持改进的部署跟踪和审核。</span><span class="sxs-lookup"><span data-stu-id="a772b-116">This connection supports improved deployment tracking and auditing.</span></span>

<span data-ttu-id="a772b-117">azure 蓝图不同于 azure 资源管理器模板。</span><span class="sxs-lookup"><span data-stu-id="a772b-117">Azure Blueprints are different from Azure Resource Manager Templates.</span></span>  <span data-ttu-id="a772b-118">当 Azure 资源管理器模板部署资源时, 它们与已部署的资源 (存在于本地环境或源控件中) 之间没有任何活动关系。</span><span class="sxs-lookup"><span data-stu-id="a772b-118">When Azure Resource Manager Templates deploy resources, they have no active relationship with the deployed resources (they exist in a local environment or source control).</span></span> <span data-ttu-id="a772b-119">相比之下, 在 azure 蓝图中, 每个部署都与一个 Azure 蓝图程序包相关联。</span><span class="sxs-lookup"><span data-stu-id="a772b-119">By contrast, with Azure Blueprint, each deployment is tied to an Azure Blueprint package.</span></span>  <span data-ttu-id="a772b-120">这意味着将维护与资源的关系, 即使在部署之后也是如此。</span><span class="sxs-lookup"><span data-stu-id="a772b-120">This means that the relationship with resources will be maintained, even after deployment.</span></span> <span data-ttu-id="a772b-121">以这种方式管理关系可改进审核和跟踪功能。</span><span class="sxs-lookup"><span data-stu-id="a772b-121">Managing relationships, in this way, improves auditing and tracking capabilities.</span></span>

<span data-ttu-id="a772b-122">azure 蓝图在 azure DevOps 方案中也很有用, 其中蓝图与特定的生成工件和发布会管道相关联, 并且可以更严格地跟踪。</span><span class="sxs-lookup"><span data-stu-id="a772b-122">Azure Blueprints are also useful in Azure DevOps scenarios, where blueprints are associated with specific build artifacts and release pipelines and can be tracked more rigorously.</span></span>