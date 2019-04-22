<span data-ttu-id="8bcdf-101">就像你的本地设备成本一样, 在使用 Azure 服务时, 会有几个元素会影响你的每月成本。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-101">Just like your on-premises equipment costs, there are several elements that will affect your monthly costs when using Azure services.</span></span> <span data-ttu-id="8bcdf-102">让我们来看看一些主要因素, 包括资源类型、服务、用户位置和帐单区域。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-102">Let's look at a few of the primary factors including resource type, services, the user's location, and the billing zone.</span></span>

### <a name="resource-type"></a><span data-ttu-id="8bcdf-103">资源类型</span><span class="sxs-lookup"><span data-stu-id="8bcdf-103">Resource type</span></span>
<span data-ttu-id="8bcdf-104">开销是特定于资源的, 因此, 计量器跟踪的使用以及与资源相关联的仪表板数取决于资源类型。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-104">Costs are resource-specific, so the usage that a meter tracks and the number of meters associated with a resource depend on the resource type.</span></span>

> [!NOTE] 
> <span data-ttu-id="8bcdf-105">每个计量器跟踪一*种特定类型的用法*。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-105">Each meter tracks a *particular kind of usage*.</span></span>  <span data-ttu-id="8bcdf-106">例如, 仪表板可能跟踪带宽使用率 (入口或出局网络流量, 以每秒位数表示)、操作数、大小 (以字节为单位的存储容量) 或类似项目。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-106">For example, a meter might track bandwidth usage (ingress or egress network traffic in bits-per-second), the number of operations, size (storage capacity in bytes), or similar items.</span></span>

<span data-ttu-id="8bcdf-107">计量器跟踪的使用情况与数量的收费单位相关联。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-107">The usage that a meter tracks correlates to a number of billable units.</span></span> <span data-ttu-id="8bcdf-108">在每个计费时段向您的帐户收取费用, 每个计费单位的费率取决于所使用的资源类型。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-108">Those are charged to your account for each billing period, and the rate per billable unit depends on the resource type you are using.</span></span>

### <a name="services"></a><span data-ttu-id="8bcdf-109">服务行业</span><span class="sxs-lookup"><span data-stu-id="8bcdf-109">Services</span></span>

:::row:::
  :::column span="3":::
<span data-ttu-id="8bcdf-110">企业、Web Direct 和云解决方案提供商 (CSP) 客户之间的 Azure 使用率和计费时段可能有所不同。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-110">Azure usage rates and billing periods can differ between Enterprise, Web Direct, and Cloud Solution Provider (CSP) customers.</span></span> <span data-ttu-id="8bcdf-111">某些订阅类型还包括影响成本的使用率余量。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-111">Some subscription types also include usage allowances, which affect costs.</span></span>

<span data-ttu-id="8bcdf-112">azure 团队开发并提供第一方产品和服务, 而来自第三方供应商的产品和服务在[Azure Marketplace](https://azuremarketplace.microsoft.com?azure-portal=true)中可用。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-112">The Azure team develops and offers first-party products and services, while products and services from third-party vendors are available in the [Azure Marketplace](https://azuremarketplace.microsoft.com?azure-portal=true).</span></span> <span data-ttu-id="8bcdf-113">不同的计费结构适用于这些类别中的每一个。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-113">Different billing structures apply to each of these categories.</span></span>
   :::column-end:::
   :::column:::

![描述了一个计费时段 (日历、计算机和计量器链接) 的图像, 说明了这三种情况之间的关联](../media/2b-billing-period-graphic.png)

   :::column-end:::
:::row-end:::

### <a name="location"></a><span data-ttu-id="8bcdf-115">位置</span><span class="sxs-lookup"><span data-stu-id="8bcdf-115">Location</span></span>
<span data-ttu-id="8bcdf-116">Azure 在世界各地都有数据中心。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-116">Azure has datacenters all over the world.</span></span> <span data-ttu-id="8bcdf-117">根据热门程度、需求和本地基础结构成本, 在提供特定 Azure 产品、服务和资源的位置之间, 使用成本有所不同。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-117">Usage costs vary between locations that offer particular Azure products, services, and resources based on popularity, demand, and local infrastructure costs.</span></span>

<span data-ttu-id="8bcdf-118">例如, 您可能希望通过在提供最低价格的位置中设置资源来生成 Azure 解决方案, 但如果从属资源及其用户位于不同的部分, 则需要在不同位置之间传输数据。范围.</span><span class="sxs-lookup"><span data-stu-id="8bcdf-118">For example, you might want to build your Azure solution by provisioning resources in locations that offer the lowest prices, but this would require transferring data between locations if dependent resources and their users are located in different parts of the world.</span></span> <span data-ttu-id="8bcdf-119">如果有仪表板跟踪在所设置的资源之间移动的数据量, 则从选择最便宜的位置进行的任何可能的节约都可能会被在这些资源之间转移数据的额外成本抵消。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-119">If there are meters tracking the volume of data that moves between the resources you provision, any potential savings you make from choosing the cheapest location could be offset by the additional cost of transferring data between those resources.</span></span>

### <a name="azure-billing-zones"></a><span data-ttu-id="8bcdf-120">Azure 计费区域</span><span class="sxs-lookup"><span data-stu-id="8bcdf-120">Azure billing zones</span></span>
<span data-ttu-id="8bcdf-121">带宽是指移动入和移出 Azure 数据中心的数据。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-121">Bandwidth refers to data moving in and out of Azure datacenters.</span></span> <span data-ttu-id="8bcdf-122">大多数时间入站数据传输 (进入 Azure 数据__ 中心的数据) 都是免费的。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-122">Most of the time inbound data transfers (data going _into_ Azure datacenters) are free.</span></span> <span data-ttu-id="8bcdf-123">对于出站数据传输 (数据__ 传出的 Azure 数据中心), 数据转让价格基于**计费区域**。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-123">For outbound data transfers (data going _out_ of Azure datacenters), the data transfer pricing is based on **Billing Zones**.</span></span>

![显示世界各地两个数据中心之间的 internet 流量的图像](../media/1b-azure-regions-globe.png)

<span data-ttu-id="8bcdf-125">**区域**是用于计费目的的 Azure 区域的地理分组。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-125">A **Zone** is a geographical grouping of Azure Regions for billing purposes.</span></span> <span data-ttu-id="8bcdf-126">以下区域存在, 并包含列出的列出的国家 (地区)。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-126">The following zones exist and include the listed countries (regions) listed.</span></span>

| <span data-ttu-id="8bcdf-127">Zone</span><span class="sxs-lookup"><span data-stu-id="8bcdf-127">Zone</span></span> | <span data-ttu-id="8bcdf-128">Areas</span><span class="sxs-lookup"><span data-stu-id="8bcdf-128">Areas</span></span> |
|------|---------|
| <span data-ttu-id="8bcdf-129">区域1</span><span class="sxs-lookup"><span data-stu-id="8bcdf-129">Zone 1</span></span> | <span data-ttu-id="8bcdf-130">美国、欧洲、加拿大、英国、法国</span><span class="sxs-lookup"><span data-stu-id="8bcdf-130">United States, Europe, Canada, UK, France</span></span> | 
| <span data-ttu-id="8bcdf-131">区域2</span><span class="sxs-lookup"><span data-stu-id="8bcdf-131">Zone 2</span></span> | <span data-ttu-id="8bcdf-132">亚太地区、日本、澳大利亚、印度、韩国</span><span class="sxs-lookup"><span data-stu-id="8bcdf-132">Asia Pacific, Japan, Australia, India, Korea</span></span> |
| <span data-ttu-id="8bcdf-133">区域3</span><span class="sxs-lookup"><span data-stu-id="8bcdf-133">Zone 3</span></span> | <span data-ttu-id="8bcdf-134">巴西</span><span class="sxs-lookup"><span data-stu-id="8bcdf-134">Brazil</span></span> |
| <span data-ttu-id="8bcdf-135">解除区域1</span><span class="sxs-lookup"><span data-stu-id="8bcdf-135">DE Zone 1</span></span> | <span data-ttu-id="8bcdf-136">德国</span><span class="sxs-lookup"><span data-stu-id="8bcdf-136">Germany</span></span> |

<span data-ttu-id="8bcdf-137">在大多数区域中, 每个月的第一个出站 5 GB 是免费的。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-137">In most zones, the first outbound 5 GB per month is free.</span></span> <span data-ttu-id="8bcdf-138">之后, 将按每 GB 的固定价格计费。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-138">After that, you are billed a fixed price per GB.</span></span>

> [!NOTE] 
> <span data-ttu-id="8bcdf-139">帐单区域不同于一个_可用性区域_。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-139">Billing zones aren't the same as an _Availability Zone_.</span></span> <span data-ttu-id="8bcdf-140">在 Azure 中, 术语 "*区域*" 仅用于帐单目的, "完整术语*可用性" 区域*是指 Azure 为数据中心提供的故障保护。</span><span class="sxs-lookup"><span data-stu-id="8bcdf-140">In Azure, the term *zone* is for billing purposes only, and the full term *Availability Zone* refers to the failure protection that Azure provides for datacenters.</span></span>