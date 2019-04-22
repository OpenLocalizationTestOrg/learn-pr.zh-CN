<span data-ttu-id="6dcec-101">我们讨论了如何通过构建高可用性、灾难恢复和备份来使应用程序可供使用和恢复。</span><span class="sxs-lookup"><span data-stu-id="6dcec-101">We've discussed how to make your application available and recoverable by architecting for high availability, disaster recovery, and backups.</span></span> <span data-ttu-id="6dcec-102">我们来看看一些关键的优势。</span><span class="sxs-lookup"><span data-stu-id="6dcec-102">Let's take a look at some of the key takeaways.</span></span>

## <a name="high-availability"></a><span data-ttu-id="6dcec-103">高可用性</span><span class="sxs-lookup"><span data-stu-id="6dcec-103">High availability</span></span>

- <span data-ttu-id="6dcec-104">高可用性是指处理系统组件的丢失或严重降级的功能。</span><span class="sxs-lookup"><span data-stu-id="6dcec-104">High availability is the ability to handle the loss or severe degradation of a component of a system.</span></span>
- <span data-ttu-id="6dcec-105">通过将重点放在以下三个关键方面来评估应用程序的高可用性:</span><span class="sxs-lookup"><span data-stu-id="6dcec-105">Evaluate your application for high availability by focusing on three key areas:</span></span>
  - <span data-ttu-id="6dcec-106">你定义的 SLA。</span><span class="sxs-lookup"><span data-stu-id="6dcec-106">Your defined SLA.</span></span>
  - <span data-ttu-id="6dcec-107">应用程序的高可用性功能。</span><span class="sxs-lookup"><span data-stu-id="6dcec-107">The HA capabilities of your application.</span></span>
  - <span data-ttu-id="6dcec-108">依赖应用程序的 HA 功能。</span><span class="sxs-lookup"><span data-stu-id="6dcec-108">The HA capabilities of dependent applications.</span></span>
- <span data-ttu-id="6dcec-109">在 Azure 上使用可用性集和可用性区域为 VM 工作负载提供 HA。</span><span class="sxs-lookup"><span data-stu-id="6dcec-109">Use availability sets and availability zones on Azure to provide HA for VM workloads.</span></span>
- <span data-ttu-id="6dcec-110">使用负载平衡服务 (如 azure 流量管理器、azure 应用程序网关和 azure 负载平衡器) 在可用系统之间分布负载。</span><span class="sxs-lookup"><span data-stu-id="6dcec-110">Use load balancing services such as Azure Traffic Manager, Azure Application Gateway, and Azure Load Balancer to distribute load across available systems.</span></span>
- <span data-ttu-id="6dcec-111">PaaS 服务具有内置的 HA, 因此可在体系结构中尽可能地利用这些服务。</span><span class="sxs-lookup"><span data-stu-id="6dcec-111">PaaS services have HA built in, so leverage these services in your architecture where possible.</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="6dcec-112">灾难恢复</span><span class="sxs-lookup"><span data-stu-id="6dcec-112">Disaster recovery</span></span>

- <span data-ttu-id="6dcec-113">灾难恢复是指从导致数据宕机和数据丢失的*影响较大的事件中恢复*。</span><span class="sxs-lookup"><span data-stu-id="6dcec-113">Disaster recovery is about *recovering from high-impact events* that result in downtime and loss of data.</span></span>
- <span data-ttu-id="6dcec-114">创建灾难恢复计划, 以定义从灾难恢复所需的过程、责任和活动。</span><span class="sxs-lookup"><span data-stu-id="6dcec-114">Create a disaster recovery plan to define the procedures, responsibilities, and activities needed to recover from a disaster.</span></span>
- <span data-ttu-id="6dcec-115">定义应用程序的 RPO 和 RTO, 以帮助确定应用程序的 DR 要求。</span><span class="sxs-lookup"><span data-stu-id="6dcec-115">Define the RPO and RTO for your application to help determine the DR requirements for your application.</span></span>
- <span data-ttu-id="6dcec-116">使用备份和复制来提供要恢复到的系统和数据的副本。</span><span class="sxs-lookup"><span data-stu-id="6dcec-116">Use backup and replication to provide copies of your systems and data to recover to.</span></span>
- <span data-ttu-id="6dcec-117">使用 Azure Site recovery 实现应用程序的 DR 进程恢复功能。</span><span class="sxs-lookup"><span data-stu-id="6dcec-117">Use Azure Site Recovery for DR process recovery capabilities for your application.</span></span>
- <span data-ttu-id="6dcec-118">测试灾难恢复计划以确定步骤的差距和相关性。</span><span class="sxs-lookup"><span data-stu-id="6dcec-118">Test your disaster recovery plan to identify gaps and relevance of steps.</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="6dcec-119">备份和还原</span><span class="sxs-lookup"><span data-stu-id="6dcec-119">Backup and restore</span></span>

- <span data-ttu-id="6dcec-120">使用备份将数据还原为灾难恢复策略的一部分或更独立的数据丢失方案。</span><span class="sxs-lookup"><span data-stu-id="6dcec-120">Use backups to restore your data as part of your DR strategy or for more isolated data loss scenarios.</span></span>
- <span data-ttu-id="6dcec-121">在本地环境中使用 Azure backup 进行完整的 VM 备份、文件和文件夹备份以及系统的备份。</span><span class="sxs-lookup"><span data-stu-id="6dcec-121">Use Azure Backup for full VM backup, file and folder backup, and backup of systems in an on-premises environment.</span></span>
- <span data-ttu-id="6dcec-122">备份功能通常内置于 PaaS 服务中, 如 azure SQL Database 和 azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="6dcec-122">Backup capabilities are often built into PaaS services, such as Azure SQL Database and Azure App Service.</span></span> <span data-ttu-id="6dcec-123">尽可能充分利用这些备份功能, 了解其默认配置和整体功能。</span><span class="sxs-lookup"><span data-stu-id="6dcec-123">Take advantage of these backup capabilities when possible, understand their default configuration and overall capabilities.</span></span>
- <span data-ttu-id="6dcec-124">定期测试还原过程和过程, 以确保它们有效且足够。</span><span class="sxs-lookup"><span data-stu-id="6dcec-124">Test your restoration processes and procedures regularly to ensure they are valid and sufficient.</span></span>
