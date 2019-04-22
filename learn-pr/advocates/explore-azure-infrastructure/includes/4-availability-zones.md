<span data-ttu-id="fc3f2-101">您需要确保您的服务和数据是冗余的, 以便您可以在出现故障时保护您的信息。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-101">You want to ensure your services and data are redundant so you can protect your information in case of failure.</span></span> <span data-ttu-id="fc3f2-102">在托管基础结构时, 需要创建重复的硬件环境。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-102">When you are hosting your infrastructure, this requires creating duplicate hardware environments.</span></span> <span data-ttu-id="fc3f2-103">Azure 可帮助您通过_可用性区域_提高应用程序的可用性。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-103">Azure can help make your app highly available through _Availability Zones_.</span></span>

## <a name="what-is-an-availability-zone"></a><span data-ttu-id="fc3f2-104">什么是可用性区域？</span><span class="sxs-lookup"><span data-stu-id="fc3f2-104">What is an Availability Zone?</span></span>

<span data-ttu-id="fc3f2-105">可用性区域在 Azure 区域中以物理方式独立于数据中心。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-105">Availability Zones are physically separate datacenters within an Azure region.</span></span>

<span data-ttu-id="fc3f2-106">每个可用性区域由一个或多个配备独立电源、冷却和网络的数据中心组成。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-106">Each Availability Zone is made up of one or more datacenters equipped with independent power, cooling, and networking.</span></span> <span data-ttu-id="fc3f2-107">它设置为_隔离边界_。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-107">It is set up to be an _isolation boundary_.</span></span> <span data-ttu-id="fc3f2-108">如果一个区域出现故障, 另一个区域将继续正常工作。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-108">If one zone goes down, the other continues working.</span></span> <span data-ttu-id="fc3f2-109">可用性区域通过高速专用光纤网络连接。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-109">Availability Zones are connected through high-speed, private fiber-optic networks.</span></span>

![显示连接到单个区域中的三个数据中心以表示可用性区域的图像](../media/4-availability-zones.png)

### <a name="supported-regions"></a><span data-ttu-id="fc3f2-111">支持的区域</span><span class="sxs-lookup"><span data-stu-id="fc3f2-111">Supported regions</span></span>

<span data-ttu-id="fc3f2-112">并不是每个区域都支持可用性区域。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-112">Not every region has support for Availability Zones.</span></span> <span data-ttu-id="fc3f2-113">以下区域至少有三个单独的区域, 以确保复原能力。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-113">The following regions have a minimum of three separate zones to ensure resiliency.</span></span>
- <span data-ttu-id="fc3f2-114">美国中部</span><span class="sxs-lookup"><span data-stu-id="fc3f2-114">Central US</span></span>
- <span data-ttu-id="fc3f2-115">美国东部2</span><span class="sxs-lookup"><span data-stu-id="fc3f2-115">East US 2</span></span>
- <span data-ttu-id="fc3f2-116">美国西部2</span><span class="sxs-lookup"><span data-stu-id="fc3f2-116">West US 2</span></span>
- <span data-ttu-id="fc3f2-117">西欧</span><span class="sxs-lookup"><span data-stu-id="fc3f2-117">West Europe</span></span>
- <span data-ttu-id="fc3f2-118">法国中部</span><span class="sxs-lookup"><span data-stu-id="fc3f2-118">France Central</span></span>
- <span data-ttu-id="fc3f2-119">北欧</span><span class="sxs-lookup"><span data-stu-id="fc3f2-119">North Europe</span></span>
- <span data-ttu-id="fc3f2-120">东南亚</span><span class="sxs-lookup"><span data-stu-id="fc3f2-120">Southeast Asia</span></span>

> [!TIP]
> <span data-ttu-id="fc3f2-121">受支持区域的列表正在扩展-请查看文档以了解最新信息。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-121">The list of supported regions is expanding - check the documentation for the latest information.</span></span>

### <a name="using-availability-zones-in-your-apps"></a><span data-ttu-id="fc3f2-122">在应用程序中使用可用性区域</span><span class="sxs-lookup"><span data-stu-id="fc3f2-122">Using Availability Zones in your apps</span></span>

<span data-ttu-id="fc3f2-123">您可以使用可用性区域运行关键任务应用程序, 并通过在区域中联合查找您的计算、存储、网络和数据资源并在其他区域中进行复制, 从而在应用程序体系结构中构建高可用性。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-123">You can use Availability Zones to run mission-critical applications and build high-availability into your application architecture by co-locating your compute, storage, networking, and data resources within a zone and replicating in other zones.</span></span> <span data-ttu-id="fc3f2-124">请记住, 在区域之间复制服务和传输数据可能会有成本。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-124">Keep in mind that there could be a cost to duplicating your services and transferring data between zones.</span></span>

<span data-ttu-id="fc3f2-125">可用性区域主要用于虚拟机、托管磁盘、负载平衡器和 SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-125">Availability Zones are primarily for VMs, managed disks, load balancers, and SQL databases.</span></span> <span data-ttu-id="fc3f2-126">支持可用性区域的 Azure 服务分为两类:</span><span class="sxs-lookup"><span data-stu-id="fc3f2-126">Azure services that support Availability Zones fall into two categories:</span></span>

- <span data-ttu-id="fc3f2-127">"**区域性服务**" –将资源固定到特定区域 (例如, 虚拟机、托管磁盘、IP 地址)</span><span class="sxs-lookup"><span data-stu-id="fc3f2-127">**Zonal services** – you pin the resource to a specific zone (for example, virtual machines, managed disks, IP addresses)</span></span>
- <span data-ttu-id="fc3f2-128">**区域冗余服务**-平台在区域之间自动复制 (例如, 区域冗余存储、SQL 数据库)。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-128">**Zone-redundant services** – platform replicates automatically across zones (for example, zone-redundant storage, SQL Database).</span></span>

<span data-ttu-id="fc3f2-129">查看文档以确定您可以将您的体系结构中的哪些元素与可用性区域相关联。</span><span class="sxs-lookup"><span data-stu-id="fc3f2-129">Check the documentation to determine which elements of your architecture you can associate with an Availability Zone.</span></span>