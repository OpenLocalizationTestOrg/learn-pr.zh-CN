<span data-ttu-id="5a8b3-101">在体系结构中包含存储性能注意事项非常重要。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-101">It's important to include storage performance considerations in your architecture.</span></span> <span data-ttu-id="5a8b3-102">就像网络延迟一样, 存储层性能较差可能会影响最终用户的体验。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-102">Just like network latency, poor performance at the storage layer can impact your end-users' experience.</span></span> <span data-ttu-id="5a8b3-103">如何优化数据存储？</span><span class="sxs-lookup"><span data-stu-id="5a8b3-103">How would you optimize your data storage?</span></span> <span data-ttu-id="5a8b3-104">您需要考虑的事项, 以确保您不会将存储瓶颈引入您的体系结构中？</span><span class="sxs-lookup"><span data-stu-id="5a8b3-104">What things do you need to consider to ensure that you're not introducing storage bottlenecks into your architecture?</span></span> <span data-ttu-id="5a8b3-105">在这里, 我们将介绍如何在体系结构中优化存储性能。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-105">Here, we'll take a look at how to optimize your storage performance in your architecture.</span></span>

## <a name="optimize-virtual-machine-storage-performance"></a><span data-ttu-id="5a8b3-106">优化虚拟机存储性能</span><span class="sxs-lookup"><span data-stu-id="5a8b3-106">Optimize virtual machine storage performance</span></span>

<span data-ttu-id="5a8b3-107">首先, 我们来看一下优化虚拟机的存储。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-107">Let's first look at optimizing storage for virtual machines.</span></span> <span data-ttu-id="5a8b3-108">磁盘存储在虚拟机的性能方面发挥着重要作用, 为应用程序选择正确的磁盘类型是一项重要决定。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-108">Disk storage plays a critical role in the performance of your virtual machines, and selecting the right disk type for your application is an important decision.</span></span>

<span data-ttu-id="5a8b3-109">不同的应用程序将具有不同的存储要求。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-109">Different applications are going to have different storage requirements.</span></span> <span data-ttu-id="5a8b3-110">您的应用程序可能对磁盘读取和写入的延迟敏感, 或者可能需要处理大量的输入/输出操作数 (IOPS) 或更高的总体磁盘吞吐量。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-110">Your application may be sensitive to latency of disk reads and writes or it may require the ability to handle a large number of input/output operations per second (IOPS) or greater overall disk throughput.</span></span>

<span data-ttu-id="5a8b3-111">构建 IaaS 工作负载时, 应使用哪种类型的磁盘？</span><span class="sxs-lookup"><span data-stu-id="5a8b3-111">When building an IaaS workload, which type of disk should you use?</span></span> <span data-ttu-id="5a8b3-112">有四个选项:</span><span class="sxs-lookup"><span data-stu-id="5a8b3-112">There are four options:</span></span>

- <span data-ttu-id="5a8b3-113">**本地 ssd 存储**-每个 VM 都有一个由本地 SSD 存储支持的临时磁盘。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-113">**Local SSD storage** - Each VM has a temporary disk that is backed by local SSD storage.</span></span> <span data-ttu-id="5a8b3-114">此磁盘的大小取决于虚拟机的大小。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-114">The size of this disk varies depending on the size of the virtual machine.</span></span> <span data-ttu-id="5a8b3-115">由于此磁盘是本地 SSD, 因此性能较高, 但在维护事件或 VM 重新部署过程中可能会丢失数据。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-115">Since this disk is local SSD, the performance is high, but data may be lost during a maintenance event or a redeployment of the VM.</span></span> <span data-ttu-id="5a8b3-116">此磁盘仅适用于临时存储不需要永久存储的数据。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-116">This disk is only suitable for temporary storage of data that you do not need permanently.</span></span> <span data-ttu-id="5a8b3-117">此磁盘非常适合于页面或交换文件, 以及 SQL Server 中的 tempdb 等内容。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-117">This disk is great for the page or swap file, and for things like tempdb in SQL Server.</span></span> <span data-ttu-id="5a8b3-118">此存储不收费。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-118">There is no charge for this storage.</span></span> <span data-ttu-id="5a8b3-119">它包括在 VM 的成本中。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-119">It's included in the cost of the VM.</span></span>

- <span data-ttu-id="5a8b3-120">**标准存储 HDD** -这是磁盘轴磁盘存储, 可适合您的应用程序不受不一致延迟或较低级别的吞吐量的限制。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-120">**Standard storage HDD** - This is spindle disk storage and may fit well where your application is not bound by inconsistent latency or lower levels of throughput.</span></span> <span data-ttu-id="5a8b3-121">对于此磁盘类型, 不需要保证性能的开发/测试工作负载是一个很好的用例。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-121">A dev/test workload where guaranteed performance isn't needed is a great use case for this disk type.</span></span>

- <span data-ttu-id="5a8b3-122">**标准存储 ssd** -这是 ssd 备份的存储, 具有有限的 ssd 延迟, 但吞吐量级别较低。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-122">**Standard storage SSD** - This is SSD backed storage and has the low latency of SSD but lower levels of throughput.</span></span> <span data-ttu-id="5a8b3-123">对于此磁盘类型, 非生产 web 服务器是一个很有用的用例。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-123">A non-production web server would be a good use case for this disk type.</span></span>

- <span data-ttu-id="5a8b3-124">**高级存储 ssd** -此 SSD 备份的存储非常适合于要投入生产的工作负载, 需要最大的可靠性和需求一致的低延迟时间, 或者需要高级别的吞吐量和 IOPS。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-124">**Premium storage SSD** - This SSD backed storage is well-suited for those workloads that are going into production, require the greatest reliability and demand consistent low latency, or need high levels of throughput and IOPS.</span></span> <span data-ttu-id="5a8b3-125">由于这些磁盘具有更高的性能和可靠性功能, 因此建议用于所有生产工作负载。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-125">Since these disks have greater performance and reliability capabilities, they are recommended for all production workloads.</span></span>

<span data-ttu-id="5a8b3-126">高级存储只能附加到特定的虚拟机 (VM) 大小。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-126">Premium storage can attach only to specific virtual machine (VM) sizes.</span></span> <span data-ttu-id="5a8b3-127">可在名称中使用 "s" 指定 "特优存储" 大小, 例如 D2**s**_v3 或 Standard_F2**s**_v2。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-127">Premium storage capable sizes are designated with an "s" in the name, for example D2**s**_v3 or Standard_F2**s**_v2.</span></span> <span data-ttu-id="5a8b3-128">任何虚拟机类型 (名称中带有或不包含 "s") 均可附加标准存储 HDD 或 SSD 驱动器。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-128">Any virtual machine type (with or without an "s" in the name) can attach standard storage HDD or SSD drives.</span></span>

<span data-ttu-id="5a8b3-129">可以使用条带技术 (如 Windows 上的 Storage Spaces Direct 或 Linux 上的 mdadm) 对磁盘进行条带化, 从而提高吞吐量和 IOPS, 具体方法是将磁盘活动分布在多个磁盘上。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-129">Disks can be striped using a striping technology (such as Storage Spaces Direct on Windows or mdadm on Linux) to increase the throughput and IOPS by spreading disk activity across multiple disks.</span></span> <span data-ttu-id="5a8b3-130">通过使用磁盘条带化, 可以真正推送磁盘的性能限制, 并且在高性能数据库系统和具有大量存储要求的其他系统中, 通常会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-130">Using disk striping allows you to really push the limits of performance for disks, and is often seen in high-performance database systems and other systems with intensive storage requirements.</span></span>

<span data-ttu-id="5a8b3-131">依赖虚拟机工作负载时, 您需要评估应用程序的性能要求, 以确定您将为虚拟机预配的基础存储。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-131">When relying on virtual machine workloads, you'll need to evaluate the performance requirements of your application to determine the underlying storage you'll provision for your virtual machines.</span></span>

## <a name="optimize-storage-performance-for-your-application"></a><span data-ttu-id="5a8b3-132">优化应用程序的存储性能</span><span class="sxs-lookup"><span data-stu-id="5a8b3-132">Optimize storage performance for your application</span></span>

<span data-ttu-id="5a8b3-133">虽然您可以使用不同的存储技术来提高原始磁盘性能, 但也可以解决在应用程序层访问数据的性能。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-133">While you can use differing storage technologies to improve the raw disk performance, you can also address the performance of access to data at the application layer.</span></span> <span data-ttu-id="5a8b3-134">让我们来看一看可执行此操作的几种方法。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-134">Let's take a look at a few ways you can do this.</span></span>

### <a name="caching"></a><span data-ttu-id="5a8b3-135">Caching</span><span class="sxs-lookup"><span data-stu-id="5a8b3-135">Caching</span></span>

<span data-ttu-id="5a8b3-136">提高应用程序性能的常用方法是在应用程序和数据存储区之间集成缓存层。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-136">A common approach to improve application performance is to integrate a caching layer between your application and your data store.</span></span> <span data-ttu-id="5a8b3-137">缓存通常将数据存储在内存中, 并允许快速检索。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-137">A cache typically stores data in memory and allows for fast retrieval.</span></span> <span data-ttu-id="5a8b3-138">此数据可以是频繁访问的数据、从数据库指定的数据或临时数据 (如用户状态)。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-138">This data can be frequently accessed data, data you specify from a database, or temporary data such as user state.</span></span> <span data-ttu-id="5a8b3-139">您可以控制所存储的数据类型、它的刷新频率以及过期时间。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-139">You'll have control over the type of data stored, how often it refreshes, and when it expires.</span></span> <span data-ttu-id="5a8b3-140">通过在与应用程序和数据库相同的区域中共同定位此缓存, 可以减少两者之间的整体延迟。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-140">By co-locating this cache in the same region as your application and database, you'll reduce the overall latency between the two.</span></span> <span data-ttu-id="5a8b3-141">将数据从缓存中提取几乎总是比从数据库检索相同数据快得多, 因此通过使用缓存层, 可以极大地提高应用程序的整体性能。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-141">Pulling data out of the cache will almost always be faster than retrieving the same data from a database, so by using a caching layer you can substantially improve the overall performance of your application.</span></span> <span data-ttu-id="5a8b3-142">下图显示了应用程序如何从数据库中检索数据, 如何将数据存储在缓存中, 并根据需要使用缓存的值。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-142">The following illustration shows how an application retrieves data from a database, stores it in a cache, and uses the cached value as needed.</span></span>

![说明从缓存检索数据比从数据库检索更快。](../media/4-cache.png)

<span data-ttu-id="5a8b3-144">Redis 的 azure 缓存是 azure 上的一种将数据存储在内存中的缓存服务。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-144">Azure Cache for Redis is a caching service on Azure that stores data in memory.</span></span> <span data-ttu-id="5a8b3-145">它基于开放源代码 Redis 缓存, 是 Microsoft 提供的完全托管服务。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-145">It's based upon the open-source Redis cache and is a fully managed service offering by Microsoft.</span></span> <span data-ttu-id="5a8b3-146">选择所需的性能层, 并将应用程序配置为使用该服务。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-146">You select the performance tier that you require and configure your application to use the service.</span></span>

### <a name="polyglot-persistence"></a><span data-ttu-id="5a8b3-147">Polyglot 持久性</span><span class="sxs-lookup"><span data-stu-id="5a8b3-147">Polyglot persistence</span></span>

<span data-ttu-id="5a8b3-148">Polyglot 持久性是使用不同的数据存储技术来处理存储要求。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-148">Polyglot persistence is the usage of different data storage technologies to handle your storage requirements.</span></span>

<span data-ttu-id="5a8b3-149">请考虑一个电子商务示例。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-149">Consider an e-commerce example.</span></span> <span data-ttu-id="5a8b3-150">您可以将应用程序资产存储在 blob 存储、在 NoSQL 存储中的产品评论和建议、以及 SQL 数据库中的用户配置文件或帐户数据。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-150">You may store application assets in a blob store, product reviews and recommendations in a NoSQL store, and user profile or account data in a SQL database.</span></span> <span data-ttu-id="5a8b3-151">下图显示了应用程序如何使用多种数据存储技术来存储不同类型的数据。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-151">The following illustration shows how an application might use multiple data storage techniques to store different types of data.</span></span>

![显示同一应用程序中不同数据存储方法的使用情况以提高性能并降低成本的插图。](../media/4-polyglotpersistence.png)

<span data-ttu-id="5a8b3-153">这一点很重要, 因为不同的数据存储区适用于某些用例, 或者因成本而更易于访问。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-153">This is important, as different data stores are designed for certain use cases or may be more accessible because of cost.</span></span> <span data-ttu-id="5a8b3-154">例如, 将 blob 存储在 SQL 数据库中可能会花费大量的访问权限, 而比从 blob 存储直接访问要慢得多。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-154">As an example, storing blobs in a SQL database may be costly and slower to access than directly from a blob store.</span></span>

<span data-ttu-id="5a8b3-155">维护跨分布式数据存储的数据一致性可能是一项重大挑战。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-155">Maintaining data consistency across distributed data stores can be a significant challenge.</span></span> <span data-ttu-id="5a8b3-156">问题在于, 只有在所有应用程序实例共享相同的数据存储区, 并且应用程序设计为确保锁定非常短的生存期时, 序列化和锁定等策略才会正常工作。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-156">The issue is that strategies such as serialization and locking only work well if all application instances share the same data store, and the application is designed to ensure that the locks are very short-lived.</span></span> <span data-ttu-id="5a8b3-157">但是, 如果在不同的数据存储区中对数据进行分区或复制, 则锁定和序列化数据访问以保持一致性可能会成为一种成本高昂的开销, 这会影响系统的吞吐量、响应时间和可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-157">However, if data is partitioned or replicated across different data stores, locking and serializing data access to maintain consistency can become an expensive overhead that impacts the throughput, response time, and scalability of a system.</span></span> <span data-ttu-id="5a8b3-158">因此, 大多数新式分布式应用程序不会锁定所修改的数据, 而是采用更宽松的一致性方法 (称为 "最终一致性")。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-158">Therefore, most modern distributed applications do not lock the data that they modify, and they take a rather more relaxed approach to consistency, known as eventual consistency.</span></span>

<span data-ttu-id="5a8b3-159">最终一致性意味着副本数据存储最终将聚合, 如果没有进一步的写入。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-159">Eventual consistency means that replica data stores will eventually converge if there are no further writes.</span></span> <span data-ttu-id="5a8b3-160">如果对其中一个数据存储区进行了写入, 则从另一个数据存储读取可能会提供略微过时的数据。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-160">If a write is made to one of the data stores, reads from another may provide slightly out-of-date data.</span></span> <span data-ttu-id="5a8b3-161">由于读取和写入操作的延迟较短, 而不是等待检查信息在所有存储中是否一致, 因此最终一致性可实现更高的扩展。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-161">Eventual consistency enables higher scale because there is a low latency for reads and writes, rather than waiting to check if information is consistent across all stores.</span></span>

## <a name="lamna-healthcare-example"></a><span data-ttu-id="5a8b3-162">Lamna 保健示例</span><span class="sxs-lookup"><span data-stu-id="5a8b3-162">Lamna Healthcare example</span></span>

<span data-ttu-id="5a8b3-163">Lamna 医疗保健的患者预定系统在两个 Azure 区域、西欧和澳大利亚东部之间托管。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-163">Lamna Healthcare's patient booking system is hosted across two Azure regions, West Europe and Australia East.</span></span> <span data-ttu-id="5a8b3-164">他们使用虚拟机作为部署其网站的前端节点, 并将 Azure SQL 数据库作为主要和澳大利亚东部部署到可读辅助副本中, 并将它们部署在西欧。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-164">They're using virtual machines as the front-end nodes to deploy their website, and have Azure SQL DB deployed in West Europe as primary and Australia East as a readable secondary.</span></span> <span data-ttu-id="5a8b3-165">他们的前端节点不需要高级别磁盘吞吐量, 但需要一致的延迟性能和生产可靠性并已使用高级 SSD 备份存储。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-165">Their front-end nodes don't require high levels of disk throughput, but do require consistent latency performance and production reliability and have used Premium SSD backed storage.</span></span>

<span data-ttu-id="5a8b3-166">他们将在每个 Azure 区域中本地托管 Redis 的 Azure 缓存, 以存储公共用户请求和医生的可用性。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-166">They are hosting an Azure Cache for Redis locally in each Azure region to store the common user requests and availability of doctors.</span></span> <span data-ttu-id="5a8b3-167">已实现缓存, 以优化应用程序上观测到的最常见数据读取活动的性能。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-167">Caching has been implemented to optimize the performance of the most common data read activities observed on the application.</span></span>

<span data-ttu-id="5a8b3-168">我们介绍了几个示例, 这些示例展示了如何在基础结构层中提高存储性能, 具体方法是在使用缓存并为数据选择适当的数据平台的情况中, 选择正确的磁盘体系结构和应用程序级别。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-168">We've covered a few examples of how you can improve storage performance in your infrastructure layer by choosing the right disk architecture and at the application level through the use of caching and selecting the right data platform for your data.</span></span> <span data-ttu-id="5a8b3-169">正确设计的解决方案将确保能够更好地执行数据访问。</span><span class="sxs-lookup"><span data-stu-id="5a8b3-169">A properly architected solution will ensure that access to data performs as well as possible.</span></span>