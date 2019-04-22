<span data-ttu-id="29efd-101">让我们先来查看你使用 Azure 的购买选项。</span><span class="sxs-lookup"><span data-stu-id="29efd-101">Let's start by examining the purchasing options you have with Azure.</span></span> <span data-ttu-id="29efd-102">有三种主要的客户类型, 可用于 Azure 产品和服务的可用购买选项是临时的, 包括:</span><span class="sxs-lookup"><span data-stu-id="29efd-102">There are three main customer types on which the available purchasing options for Azure products and services are contingent, including:</span></span>

- <span data-ttu-id="29efd-103">**企业**客户-使用 azure 对企业协议进行签名, 以提交这些协议以在 azure 服务上进行协商, 这通常每年支付一起来。</span><span class="sxs-lookup"><span data-stu-id="29efd-103">**Enterprise** - Enterprise customers sign an Enterprise Agreement with Azure that commits them to spend a negotiated amount on Azure services, which they typically pay annually.</span></span> <span data-ttu-id="29efd-104">企业客户还可以访问自定义的 Azure 定价。</span><span class="sxs-lookup"><span data-stu-id="29efd-104">Enterprise customers also have access to customized Azure pricing.</span></span>
- <span data-ttu-id="29efd-105">**web direct** direct web 客户支付了 azure 资源的一般公共价格, 并通过 azure 网站进行了每月的帐单和付款。</span><span class="sxs-lookup"><span data-stu-id="29efd-105">**Web direct** - Direct Web customers pay general public prices for Azure resources, and their monthly billing and payments occur through the Azure website.</span></span>
- <span data-ttu-id="29efd-106">**云解决方案提供商**-云解决方案提供商 (CSP) 通常是指客户雇用在 Azure 之上构建解决方案的 Microsoft 合作伙伴公司。</span><span class="sxs-lookup"><span data-stu-id="29efd-106">**Cloud Solution Provider** - Cloud Solution Provider (CSP) typically are Microsoft partner companies that a customer hires to build solutions on top of Azure.</span></span> <span data-ttu-id="29efd-107">Azure 使用情况的付款和帐单通过客户的 CSP 进行。</span><span class="sxs-lookup"><span data-stu-id="29efd-107">Payment and billing for Azure usage occur through the customer's CSP.</span></span>

![各种 Azure 订阅选项的描述](../media/1a-subscription-options.png)

<span data-ttu-id="29efd-109">Azure 中的产品和服务按类别进行排列, 其中包含可预配的各种资源。</span><span class="sxs-lookup"><span data-stu-id="29efd-109">Products and services in Azure are arranged by category, which has various resources that you can provision.</span></span> <span data-ttu-id="29efd-110">你可以选择符合你的要求的 Azure 产品和服务, 你的帐户将根据 Azure 的付费使用模式进行计费。</span><span class="sxs-lookup"><span data-stu-id="29efd-110">You select the Azure products and services that fit your requirements, and your account is billed according to Azure's pay-for-what-you-use model.</span></span>

![显示具有特色产品选择的各种 Azure 产品的描述, 并显示这些产品的名称和简短说明](../media/1a-Azure-products-overview.png)

### <a name="usage-meters"></a><span data-ttu-id="29efd-112">使用计量器</span><span class="sxs-lookup"><span data-stu-id="29efd-112">Usage meters</span></span>

<span data-ttu-id="29efd-113">预配 azure 资源时, azure 将为该资源创建一个或多个计量器实例。</span><span class="sxs-lookup"><span data-stu-id="29efd-113">When you provision an Azure resource, Azure creates one or more meter instances for that resource.</span></span> <span data-ttu-id="29efd-114">计量器跟踪资源的使用情况, 并生成用于计算您的帐单的使用率记录。</span><span class="sxs-lookup"><span data-stu-id="29efd-114">The meters track the resources' usage, and generate a usage record that is used to calculate your bill.</span></span>

<span data-ttu-id="29efd-115">例如, 在 Azure 中预配的单个虚拟机可能会有以下计量器跟踪其使用情况:</span><span class="sxs-lookup"><span data-stu-id="29efd-115">For example, a single virtual machine that you provision in Azure might have the following meters tracking its usage:</span></span>

:::row:::
  :::column:::
- <span data-ttu-id="29efd-116">计算小时数</span><span class="sxs-lookup"><span data-stu-id="29efd-116">Compute Hours</span></span>
- <span data-ttu-id="29efd-117">IP 地址小时数</span><span class="sxs-lookup"><span data-stu-id="29efd-117">IP Address Hours</span></span>
- <span data-ttu-id="29efd-118">中的数据传输</span><span class="sxs-lookup"><span data-stu-id="29efd-118">Data Transfer In</span></span>
- <span data-ttu-id="29efd-119">数据传出</span><span class="sxs-lookup"><span data-stu-id="29efd-119">Data Transfer Out</span></span>
- <span data-ttu-id="29efd-120">标准托管磁盘</span><span class="sxs-lookup"><span data-stu-id="29efd-120">Standard Managed Disk</span></span>
  :::column-end:::
  :::column:::
- <span data-ttu-id="29efd-121">标准托管磁盘操作</span><span class="sxs-lookup"><span data-stu-id="29efd-121">Standard Managed Disk Operations</span></span>
- <span data-ttu-id="29efd-122">标准 IO-磁盘</span><span class="sxs-lookup"><span data-stu-id="29efd-122">Standard IO-Disk</span></span>
- <span data-ttu-id="29efd-123">标准 IO 块 Blob 读取</span><span class="sxs-lookup"><span data-stu-id="29efd-123">Standard IO-Block Blob Read</span></span>
- <span data-ttu-id="29efd-124">标准 IO 块 Blob 写入</span><span class="sxs-lookup"><span data-stu-id="29efd-124">Standard IO-Block Blob Write</span></span>
- <span data-ttu-id="29efd-125">标准 IO 块 Blob 删除</span><span class="sxs-lookup"><span data-stu-id="29efd-125">Standard IO-Block Blob Delete</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="29efd-126">仪表盘和定价因每个产品而异, 并且根据资源的大小或容量, 通常具有不同的定价层。</span><span class="sxs-lookup"><span data-stu-id="29efd-126">The meters and pricing vary per product and often have different pricing tiers based on the size or capacity of the resource.</span></span> <span data-ttu-id="29efd-127">查看文档以了解有关每个服务区域成本的具体详细信息。</span><span class="sxs-lookup"><span data-stu-id="29efd-127">Check the documentation for specific details on what each service area costs.</span></span>

<span data-ttu-id="29efd-128">每月记帐周期结束时, 使用值将收取您的付款方式, 并会重置仪表。</span><span class="sxs-lookup"><span data-stu-id="29efd-128">At the end of each monthly billing cycle, the usage values will be charged to your payment method and the meters are reset.</span></span> <span data-ttu-id="29efd-129">您可以随时检查 Azure 门户中的帐单页面, 以获取当前使用情况的快速摘要, 以及从过去的记帐周期更改的任何发票。</span><span class="sxs-lookup"><span data-stu-id="29efd-129">You can check the billing page in the Azure portal at any time to get a quick summary of your current usage, as well as any invoices changed from past billing cycles.</span></span> 

<span data-ttu-id="29efd-130">关键好处在于是始终_根据使用情况_收取资源。</span><span class="sxs-lookup"><span data-stu-id="29efd-130">The key takeaway is that resources are always charged _based on usage_.</span></span> <span data-ttu-id="29efd-131">例如, 如果您取消分配虚拟机, 则不会对计算时间、i/o 读取或写入或 IP 地址计费, 因为 vm 未运行且没有已分配的计算资源。</span><span class="sxs-lookup"><span data-stu-id="29efd-131">For example, if you de-allocate a VM then you will not be billed for compute hours, I/O reads or writes or the IP address since the VM is not running and has no allocated compute resources.</span></span> <span data-ttu-id="29efd-132">不过, 你将会承担磁盘的存储成本。</span><span class="sxs-lookup"><span data-stu-id="29efd-132">However you will incur storage costs for the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="29efd-133">取消分配 vm 与_删除_vm 不同。</span><span class="sxs-lookup"><span data-stu-id="29efd-133">De-allocating a VM is not the same as _deleting_ a VM.</span></span> <span data-ttu-id="29efd-134">"取消分配" 意味着未将 VM 分配到数据中心中的 CPU 或网络。</span><span class="sxs-lookup"><span data-stu-id="29efd-134">De-allocation means the VM is not assigned to a CPU or network in a datacenter.</span></span> <span data-ttu-id="29efd-135">但是, 您的持久性磁盘仍然存在, 并且您的订阅中存在该资源。</span><span class="sxs-lookup"><span data-stu-id="29efd-135">However, your persistent disks remain, and the resource is present in your subscription.</span></span> <span data-ttu-id="29efd-136">这类似于关闭物理计算机。</span><span class="sxs-lookup"><span data-stu-id="29efd-136">It's similar to turning off your physical computer.</span></span> 