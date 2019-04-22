<span data-ttu-id="ea79f-101">我们已讨论的存储帐户设置适用于帐户中的数据服务。</span><span class="sxs-lookup"><span data-stu-id="ea79f-101">The storage account settings we've already covered apply to the data services in the account.</span></span> <span data-ttu-id="ea79f-102">在这里, 我们将讨论适用于帐户本身的三个设置, 而不是存储在帐户中的数据:</span><span class="sxs-lookup"><span data-stu-id="ea79f-102">Here, we will discuss the three settings that apply to the account itself, rather than to the data stored in the account:</span></span>

- <span data-ttu-id="ea79f-103">名称</span><span class="sxs-lookup"><span data-stu-id="ea79f-103">Name</span></span>
- <span data-ttu-id="ea79f-104">部署模型</span><span class="sxs-lookup"><span data-stu-id="ea79f-104">Deployment model</span></span>
- <span data-ttu-id="ea79f-105">帐户种类</span><span class="sxs-lookup"><span data-stu-id="ea79f-105">Account kind</span></span>

<span data-ttu-id="ea79f-106">这些设置会影响您管理帐户的方式以及服务中服务的成本。</span><span class="sxs-lookup"><span data-stu-id="ea79f-106">These settings impact how you manage your account and the cost of the services within it.</span></span>

## <a name="name"></a><span data-ttu-id="ea79f-107">名称</span><span class="sxs-lookup"><span data-stu-id="ea79f-107">Name</span></span>

<span data-ttu-id="ea79f-108">每个存储帐户都有一个名称。</span><span class="sxs-lookup"><span data-stu-id="ea79f-108">Each storage account has a name.</span></span> <span data-ttu-id="ea79f-109">该名称在 Azure 中必须是全局唯一的, 只能使用小写字母和数字, 并且必须介于3到24个字符之间。</span><span class="sxs-lookup"><span data-stu-id="ea79f-109">The name must be globally unique within Azure, use only lowercase letters and digits and be between 3 and 24 characters.</span></span>

## <a name="deployment-model"></a><span data-ttu-id="ea79f-110">部署模型</span><span class="sxs-lookup"><span data-stu-id="ea79f-110">Deployment model</span></span>

<span data-ttu-id="ea79f-111">系统 Azure 使用_部署模型_来组织资源。</span><span class="sxs-lookup"><span data-stu-id="ea79f-111">A _deployment model_ is the system Azure uses to organize your resources.</span></span> <span data-ttu-id="ea79f-112">模型定义用于创建、配置和管理这些资源的 API。</span><span class="sxs-lookup"><span data-stu-id="ea79f-112">The model defines the API that you use to create, configure, and manage those resources.</span></span> <span data-ttu-id="ea79f-113">Azure 提供了两种部署模型:</span><span class="sxs-lookup"><span data-stu-id="ea79f-113">Azure provides two deployment models:</span></span>

- <span data-ttu-id="ea79f-114">**资源管理器**: 使用 Azure 资源管理器 API 的当前模型</span><span class="sxs-lookup"><span data-stu-id="ea79f-114">**Resource Manager**: the current model that uses the Azure Resource Manager API</span></span>
- <span data-ttu-id="ea79f-115">**经典**: 使用 Azure 服务管理 API 的旧版产品</span><span class="sxs-lookup"><span data-stu-id="ea79f-115">**Classic**: a legacy offering that uses the Azure Service Management API</span></span>

<span data-ttu-id="ea79f-116">决定选择哪一项通常很简单, 因为大多数 Azure 资源仅适用于资源管理器。</span><span class="sxs-lookup"><span data-stu-id="ea79f-116">The decision on which one to choose is usually easy, because most Azure resources only work with Resource Manager.</span></span> <span data-ttu-id="ea79f-117">但是, 存储帐户、虚拟机和虚拟网络支持这两种情况, 因此在创建存储帐户时必须选择其中一个或另一个。</span><span class="sxs-lookup"><span data-stu-id="ea79f-117">However, storage accounts, virtual machines, and virtual networks support both, so you must choose one or the other when you create your storage account.</span></span>

<span data-ttu-id="ea79f-118">这两个模型之间的主要功能差异在于它们对分组的支持。</span><span class="sxs-lookup"><span data-stu-id="ea79f-118">The key feature difference between the two models is their support for grouping.</span></span> <span data-ttu-id="ea79f-119">资源管理器模型添加了_资源组_的概念, 该概念在经典模型中不可用。</span><span class="sxs-lookup"><span data-stu-id="ea79f-119">The Resource Manager model adds the concept of a _resource group_, which is not available in the classic model.</span></span> <span data-ttu-id="ea79f-120">使用资源组, 可以将资源集合作为一个单元进行部署和管理。</span><span class="sxs-lookup"><span data-stu-id="ea79f-120">A resource group lets you deploy and manage a collection of resources as a single unit.</span></span>

<span data-ttu-id="ea79f-121">Microsoft 建议您对所有新资源使用**资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="ea79f-121">Microsoft recommends that you use **Resource Manager** for all new resources.</span></span>

## <a name="account-kind"></a><span data-ttu-id="ea79f-122">帐户种类</span><span class="sxs-lookup"><span data-stu-id="ea79f-122">Account kind</span></span>

<span data-ttu-id="ea79f-123">存储帐户_种类_是一组策略, 用于确定可以在帐户中包括哪些数据服务以及这些服务的定价。</span><span class="sxs-lookup"><span data-stu-id="ea79f-123">Storage account _kind_ is a set of policies that determine which data services you can include in the account and the pricing of those services.</span></span> <span data-ttu-id="ea79f-124">有三种类型的存储帐户:</span><span class="sxs-lookup"><span data-stu-id="ea79f-124">There are three kinds of storage accounts:</span></span>

- <span data-ttu-id="ea79f-125">**StorageV2 (常规用途 v2)**: 支持所有存储类型和所有最新功能的当前服务</span><span class="sxs-lookup"><span data-stu-id="ea79f-125">**StorageV2 (general purpose v2)**: the current offering that supports all storage types and all of the latest features</span></span>
- <span data-ttu-id="ea79f-126">**Storage (常规目的 v1)**: 一种支持所有存储类型但可能不支持所有功能的旧类型</span><span class="sxs-lookup"><span data-stu-id="ea79f-126">**Storage (general purpose v1)**: a legacy kind that supports all storage types but may not support all features</span></span>
- <span data-ttu-id="ea79f-127">**Blob 存储**: 仅允许块 blob 和追加 blob 的旧版类型</span><span class="sxs-lookup"><span data-stu-id="ea79f-127">**Blob storage**: a legacy kind that allows only block blobs and append blobs</span></span>

<span data-ttu-id="ea79f-128">Microsoft 建议对新存储帐户使用**通用 v2**选项。</span><span class="sxs-lookup"><span data-stu-id="ea79f-128">Microsoft recommends that you use the **General-purpose v2** option for new storage accounts.</span></span>

<span data-ttu-id="ea79f-129">有几种特殊情况可能是此规则的例外。</span><span class="sxs-lookup"><span data-stu-id="ea79f-129">There are a few special cases that can be exceptions to this rule.</span></span> <span data-ttu-id="ea79f-130">例如, 交易的定价低于常规目的 v1, 这样, 您就可以略微降低成本 (如果符合您的典型工作负载)。</span><span class="sxs-lookup"><span data-stu-id="ea79f-130">For example, pricing for transactions is lower in general purpose v1, which would allow you to slightly reduce costs if that matches your typical workload.</span></span>

<span data-ttu-id="ea79f-131">此处的核心建议是为你的所有存储帐户选择**资源管理器**部署模型和**StorageV2 (常规用途 v2)** 帐户类型。</span><span class="sxs-lookup"><span data-stu-id="ea79f-131">The core advice here is to choose the **Resource Manager** deployment model and the **StorageV2 (general purpose v2)** account kind for all your storage accounts.</span></span> <span data-ttu-id="ea79f-132">其他选项仍然存在, 主要是允许现有资源继续运行。</span><span class="sxs-lookup"><span data-stu-id="ea79f-132">The other options still exist primarily to allow existing resources to continue operation.</span></span> <span data-ttu-id="ea79f-133">对于新资源, 有几个原因需要考虑其他选择。</span><span class="sxs-lookup"><span data-stu-id="ea79f-133">For new resources, there are few reasons to consider the other choices.</span></span>