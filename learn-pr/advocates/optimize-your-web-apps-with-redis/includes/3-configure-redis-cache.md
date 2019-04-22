<span data-ttu-id="fedbf-101">您的体育统计信息开发团队已决定缓存可显著提高最近请求的数据的性能。</span><span class="sxs-lookup"><span data-stu-id="fedbf-101">Your sports statistics development team has decided that caching could dramatically improve performance for recently requested data.</span></span> <span data-ttu-id="fedbf-102">下一步是为 Redis 实例创建和配置 Azure 缓存。</span><span class="sxs-lookup"><span data-stu-id="fedbf-102">Your next step is to create and configure an Azure Cache for Redis instance.</span></span>

## <a name="create-and-configure-the-azure-cache-for-redis-instance"></a><span data-ttu-id="fedbf-103">创建和配置 Redis 实例的 Azure 缓存</span><span class="sxs-lookup"><span data-stu-id="fedbf-103">Create and configure the Azure Cache for Redis instance</span></span>

<span data-ttu-id="fedbf-104">您可以使用 azure 门户、azure CLI 或 azure PowerShell 创建 Redis 缓存。</span><span class="sxs-lookup"><span data-stu-id="fedbf-104">You can create a Redis cache using the Azure portal, the Azure CLI, or Azure PowerShell.</span></span> <span data-ttu-id="fedbf-105">您需要确定几个参数, 以便正确配置缓存以满足您的需求。</span><span class="sxs-lookup"><span data-stu-id="fedbf-105">There are several parameters you will need to decide in order to configure the cache properly for your purposes.</span></span>

### <a name="name"></a><span data-ttu-id="fedbf-106">名称</span><span class="sxs-lookup"><span data-stu-id="fedbf-106">Name</span></span>

<span data-ttu-id="fedbf-107">Redis 缓存将需要一个全局唯一名称。</span><span class="sxs-lookup"><span data-stu-id="fedbf-107">The Redis cache will need a globally unique name.</span></span> <span data-ttu-id="fedbf-108">名称在 Azure 中必须是唯一的, 因为它用于生成面向公众的 URL 以连接服务并与之通信。</span><span class="sxs-lookup"><span data-stu-id="fedbf-108">The name has to be unique within Azure because it is used to generate a public-facing URL to connect and communicate with the service.</span></span>

<span data-ttu-id="fedbf-109">名称必须介于1到63个字符之间, 由数字、字母和 '-' 字符组成。</span><span class="sxs-lookup"><span data-stu-id="fedbf-109">The name must be between 1 and 63 characters, composed of numbers, letters, and the '-' character.</span></span> <span data-ttu-id="fedbf-110">缓存名称不能以 "-" 字符开头或结尾, 且连续的 "-" 字符无效。</span><span class="sxs-lookup"><span data-stu-id="fedbf-110">The cache name can't start or end with the '-' character, and consecutive '-' characters aren't valid.</span></span>

### <a name="resource-group"></a><span data-ttu-id="fedbf-111">资源组</span><span class="sxs-lookup"><span data-stu-id="fedbf-111">Resource Group</span></span>

<span data-ttu-id="fedbf-112">Redis 的 Azure 缓存是一个托管资源, 需要_资源组_所有者。</span><span class="sxs-lookup"><span data-stu-id="fedbf-112">The Azure Cache for Redis is a managed resource and needs a _resource group_ owner.</span></span> <span data-ttu-id="fedbf-113">您可以创建新的资源组, 也可以在您所属的订阅中使用现有资源组。</span><span class="sxs-lookup"><span data-stu-id="fedbf-113">You can either create a new resource group, or use an existing one in a subscription you are part of.</span></span>

### <a name="location"></a><span data-ttu-id="fedbf-114">位置</span><span class="sxs-lookup"><span data-stu-id="fedbf-114">Location</span></span>

<span data-ttu-id="fedbf-115">您将需要通过选择 Azure 区域来决定 Redis 缓存的物理位置。</span><span class="sxs-lookup"><span data-stu-id="fedbf-115">You will need to decide where the Redis cache will be physically located by selecting an Azure region.</span></span> <span data-ttu-id="fedbf-116">应始终将缓存实例和应用程序放在同一区域中。</span><span class="sxs-lookup"><span data-stu-id="fedbf-116">You should always place your cache instance and your application in the same region.</span></span> <span data-ttu-id="fedbf-117">连接到不同区域中的缓存会显著增加延迟并降低可靠性。</span><span class="sxs-lookup"><span data-stu-id="fedbf-117">Connecting to a cache in a different region can significantly increase latency and reduce reliability.</span></span> <span data-ttu-id="fedbf-118">如果要连接到 Azure 外部的缓存, 请选择要在使用数据的应用程序运行的位置附近的位置。</span><span class="sxs-lookup"><span data-stu-id="fedbf-118">If you are connecting to the cache outside of Azure, then select a location close to where the application consuming the data is running.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fedbf-119">尽可能将 Redis 缓存放在数据_使用者_附近。</span><span class="sxs-lookup"><span data-stu-id="fedbf-119">Put the Redis cache as close to the data _consumer_ as you can.</span></span>

### <a name="pricing-tier"></a><span data-ttu-id="fedbf-120">定价层</span><span class="sxs-lookup"><span data-stu-id="fedbf-120">Pricing tier</span></span>

<span data-ttu-id="fedbf-121">如最后一个设备中所述, 有三个可用于 Redis 的 Azure 缓存定价层。</span><span class="sxs-lookup"><span data-stu-id="fedbf-121">As mentioned in the last unit, there are three pricing tiers available for an Azure Cache for Redis.</span></span>

- <span data-ttu-id="fedbf-122">**基本**: 适用于开发/测试的基本缓存。</span><span class="sxs-lookup"><span data-stu-id="fedbf-122">**Basic**: Basic cache ideal for development/testing.</span></span> <span data-ttu-id="fedbf-123">限制为单个服务器、53 GB 的内存和20000连接。</span><span class="sxs-lookup"><span data-stu-id="fedbf-123">Is limited to a single server, 53 GB of memory, and 20,000 connections.</span></span> <span data-ttu-id="fedbf-124">此服务层没有 SLA。</span><span class="sxs-lookup"><span data-stu-id="fedbf-124">There is no SLA for this service tier.</span></span>
- <span data-ttu-id="fedbf-125">**标准**: 支持复制的生产缓存, 并包含 99.99% SLA。</span><span class="sxs-lookup"><span data-stu-id="fedbf-125">**Standard**: Production cache which supports replication and includes an 99.99% SLA.</span></span> <span data-ttu-id="fedbf-126">它支持两台服务器 (主/从), 并具有与基本层相同的内存/连接限制。</span><span class="sxs-lookup"><span data-stu-id="fedbf-126">It supports two servers (master/slave), and has the same memory/connection limits as the Basic tier.</span></span>
- <span data-ttu-id="fedbf-127">**Premium**: 在标准层上构建的企业级, 包括暂留、聚集和扩展缓存支持。</span><span class="sxs-lookup"><span data-stu-id="fedbf-127">**Premium**: Enterprise tier which builds on the Standard tier and includes persistence, clustering, and scale-out cache support.</span></span> <span data-ttu-id="fedbf-128">这是具有高达 530 GB 内存和40000同时连接的高性能层。</span><span class="sxs-lookup"><span data-stu-id="fedbf-128">This is the highest performing tier with up to 530 GB of memory and 40,000 simultaneous connections.</span></span>

<span data-ttu-id="fedbf-129">您可以控制每个层上可用的缓存内存量-这是通过从 C0-C6 为 Basic/Standard 和 P0-P4 为 Premium 选择缓存级别选择的。</span><span class="sxs-lookup"><span data-stu-id="fedbf-129">You can control the amount of cache memory available on each tier - this is selected by choosing a cache level from C0-C6 for Basic/Standard and P0-P4 for Premium.</span></span> <span data-ttu-id="fedbf-130">有关详细信息, 请查看 "[定价" 页面](https://azure.microsoft.com/pricing/details/cache/)。</span><span class="sxs-lookup"><span data-stu-id="fedbf-130">Check the [pricing page](https://azure.microsoft.com/pricing/details/cache/) for full details.</span></span>

> [!TIP]
> <span data-ttu-id="fedbf-131">Microsoft 建议您始终对生产系统使用标准或高级层。</span><span class="sxs-lookup"><span data-stu-id="fedbf-131">Microsoft recommends you always use Standard or Premium Tier for production systems.</span></span> <span data-ttu-id="fedbf-132">基本层是单个节点系统, 无数据复制和无 SLA。</span><span class="sxs-lookup"><span data-stu-id="fedbf-132">The Basic Tier is a single node system with no data replication and no SLA.</span></span> <span data-ttu-id="fedbf-133">此外, 至少使用 C1 缓存。</span><span class="sxs-lookup"><span data-stu-id="fedbf-133">Also, use at least a C1 cache.</span></span> <span data-ttu-id="fedbf-134">C0 缓存实际上适用于简单的开发/测试方案, 因为它们具有共享的 CPU 内核和非常少的内存。</span><span class="sxs-lookup"><span data-stu-id="fedbf-134">C0 caches are really meant for simple dev/test scenarios since they have a shared CPU core and very little memory.</span></span>

<span data-ttu-id="fedbf-135">高级层允许您以两种方式保留数据, 以提供灾难恢复:</span><span class="sxs-lookup"><span data-stu-id="fedbf-135">The Premium tier allows you to persist data in two ways to provide disaster recovery:</span></span>

1. <span data-ttu-id="fedbf-136">RDB 持久化采用定期快照, 并且可以在出现故障时使用快照重建缓存。</span><span class="sxs-lookup"><span data-stu-id="fedbf-136">RDB persistence takes a periodic snapshot and can rebuild the cache using the snapshot in case of failure.</span></span>

    ![在新的 Redis 缓存实例上显示 RDB 持久性选项的 Azure 门户屏幕截图。](../media/3-redis-persistence-1.png)

2. <span data-ttu-id="fedbf-138">AOF 持久性将每个写入操作保存到每秒至少保存一次的日志。</span><span class="sxs-lookup"><span data-stu-id="fedbf-138">AOF persistence saves every write operation to a log that is saved at least once per second.</span></span> <span data-ttu-id="fedbf-139">这将创建比 RDB 更大的文件, 但数据丢失较少。</span><span class="sxs-lookup"><span data-stu-id="fedbf-139">This creates bigger files than RDB but has less data loss.</span></span>

    ![显示新 Redis 缓存实例上的 AOF 持久性选项的 Azure 门户屏幕截图。](../media/3-redis-persistence-2.png)

<span data-ttu-id="fedbf-141">有几个其他设置仅适用于**高级**层。</span><span class="sxs-lookup"><span data-stu-id="fedbf-141">There are several other settings which are only available to the **Premium** tier.</span></span>

### <a name="virtual-network-support"></a><span data-ttu-id="fedbf-142">虚拟网络支持</span><span class="sxs-lookup"><span data-stu-id="fedbf-142">Virtual Network support</span></span>

<span data-ttu-id="fedbf-143">如果创建高级层 Redis 缓存, 则可以将其部署到云中的虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="fedbf-143">If you create a premium tier Redis cache, you can deploy it to a virtual network in the cloud.</span></span> <span data-ttu-id="fedbf-144">您的缓存将仅对同一虚拟网络中的其他虚拟机和应用程序可用。</span><span class="sxs-lookup"><span data-stu-id="fedbf-144">Your cache will be available to only other virtual machines and applications in the same virtual network.</span></span> <span data-ttu-id="fedbf-145">当您的服务和缓存托管在 azure 中, 或通过 azure 虚拟网络 VPN 连接时, 这将提供更高级别的安全性。</span><span class="sxs-lookup"><span data-stu-id="fedbf-145">This provides a higher level of security when your service and cache are both hosted in Azure, or are connected through an Azure virtual network VPN.</span></span>

### <a name="clustering-support"></a><span data-ttu-id="fedbf-146">群集支持</span><span class="sxs-lookup"><span data-stu-id="fedbf-146">Clustering support</span></span>

<span data-ttu-id="fedbf-147">使用高级层 Redis 缓存, 可以实现群集以在多个节点之间自动拆分数据集。</span><span class="sxs-lookup"><span data-stu-id="fedbf-147">With a premium tier Redis cache, you can implement clustering to automatically split your dataset among multiple nodes.</span></span> <span data-ttu-id="fedbf-148">若要实施群集, 请指定最大值为10的 shards 数。</span><span class="sxs-lookup"><span data-stu-id="fedbf-148">To implement clustering, you specify the number of shards to a maximum of 10.</span></span> <span data-ttu-id="fedbf-149">产生的成本是原始节点的成本, 乘以 shards 的数量。</span><span class="sxs-lookup"><span data-stu-id="fedbf-149">The cost incurred is the cost of the original node, multiplied by the number of shards.</span></span>

## <a name="accessing-the-redis-instance"></a><span data-ttu-id="fedbf-150">访问 Redis 实例</span><span class="sxs-lookup"><span data-stu-id="fedbf-150">Accessing the Redis instance</span></span>

<span data-ttu-id="fedbf-151">Redis 支持一组[已知命令](https://redis.io/commands)。</span><span class="sxs-lookup"><span data-stu-id="fedbf-151">Redis supports a set of [known commands](https://redis.io/commands).</span></span> <span data-ttu-id="fedbf-152">通常将命令作为`COMMAND parameter1 parameter2 parameter3`发出。</span><span class="sxs-lookup"><span data-stu-id="fedbf-152">A command is typically issued as `COMMAND parameter1 parameter2 parameter3`.</span></span>

<span data-ttu-id="fedbf-153">以下是您可以使用的一些常见命令:</span><span class="sxs-lookup"><span data-stu-id="fedbf-153">Here are some common commands you can use:</span></span>

| <span data-ttu-id="fedbf-154">指挥</span><span class="sxs-lookup"><span data-stu-id="fedbf-154">Command</span></span> | <span data-ttu-id="fedbf-155">说明</span><span class="sxs-lookup"><span data-stu-id="fedbf-155">Description</span></span> |
|---------|-------------|
| `ping` | <span data-ttu-id="fedbf-156">Ping 服务器。</span><span class="sxs-lookup"><span data-stu-id="fedbf-156">Ping the server.</span></span> <span data-ttu-id="fedbf-157">返回 "乒乓球"。</span><span class="sxs-lookup"><span data-stu-id="fedbf-157">Returns "PONG".</span></span> |
| `set [key] [value]` | <span data-ttu-id="fedbf-158">在缓存中设置键/值。</span><span class="sxs-lookup"><span data-stu-id="fedbf-158">Sets a key/value in the cache.</span></span> <span data-ttu-id="fedbf-159">成功后返回 "确定"。</span><span class="sxs-lookup"><span data-stu-id="fedbf-159">Returns "OK" on success.</span></span> |
| `get [key]` | <span data-ttu-id="fedbf-160">从缓存中获取值。</span><span class="sxs-lookup"><span data-stu-id="fedbf-160">Gets a value from the cache.</span></span> |
| `exists [key]` | <span data-ttu-id="fedbf-161">如果**项**在缓存中存在, 则返回 "1", 如果不存在, 则返回 "0"。</span><span class="sxs-lookup"><span data-stu-id="fedbf-161">Returns '1' if the **key** exists in the cache, '0' if it doesn't.</span></span> |
| `type [key]` | <span data-ttu-id="fedbf-162">返回与给定**键**的值关联的类型。</span><span class="sxs-lookup"><span data-stu-id="fedbf-162">Returns the type associated to the value for the given **key**.</span></span> |
| `incr [key]` | <span data-ttu-id="fedbf-163">将与**键**关联的给定值递增 "1"。</span><span class="sxs-lookup"><span data-stu-id="fedbf-163">Increment the given value associated with **key** by '1'.</span></span> <span data-ttu-id="fedbf-164">值必须为整数或双精度值。</span><span class="sxs-lookup"><span data-stu-id="fedbf-164">The value must be an integer or double value.</span></span> <span data-ttu-id="fedbf-165">这将返回新值。</span><span class="sxs-lookup"><span data-stu-id="fedbf-165">This returns the new value.</span></span> |
| `incrby [key] [amount]` | <span data-ttu-id="fedbf-166">将与**键**关联的给定值递增指定的量。</span><span class="sxs-lookup"><span data-stu-id="fedbf-166">Increment the given value associated with **key** by the specified amount.</span></span> <span data-ttu-id="fedbf-167">值必须为整数或双精度值。</span><span class="sxs-lookup"><span data-stu-id="fedbf-167">The value must be an integer or double value.</span></span> <span data-ttu-id="fedbf-168">这将返回新值。</span><span class="sxs-lookup"><span data-stu-id="fedbf-168">This returns the new value.</span></span> |
| `del [key]` | <span data-ttu-id="fedbf-169">删除与**键**关联的值。</span><span class="sxs-lookup"><span data-stu-id="fedbf-169">Deletes the value associated with the **key**.</span></span> |
| `flushdb` | <span data-ttu-id="fedbf-170">删除数据库中的_所有_键和值。</span><span class="sxs-lookup"><span data-stu-id="fedbf-170">Delete _all_ keys and values in the database.</span></span> |

<span data-ttu-id="fedbf-171">Redis 有一个命令行工具 (**Redis-cli**), 您可以使用它直接试用这些命令。</span><span class="sxs-lookup"><span data-stu-id="fedbf-171">Redis has a command-line tool (**redis-cli**) you can use to experiment directly with these commands.</span></span> <span data-ttu-id="fedbf-172">下面是一些示例。</span><span class="sxs-lookup"><span data-stu-id="fedbf-172">Here are some examples.</span></span>

```output
> set somekey somevalue
OK
> get somekey
"somevalue"
> exists somekey
(string) 1
> del somekey
(string) 1
> exists somekey
(string) 0
```

<span data-ttu-id="fedbf-173">下面的示例展示了如何使用`INCR`命令。</span><span class="sxs-lookup"><span data-stu-id="fedbf-173">Here's an example of working with the `INCR` commands.</span></span> <span data-ttu-id="fedbf-174">这是很方便的, 因为它们在使用缓存的_多个应用程序之间_提供了原子增量。</span><span class="sxs-lookup"><span data-stu-id="fedbf-174">These are convenient because they provide atomic increments _across multiple applications_ that are using the cache.</span></span>

```output
> set counter 100
OK
> incr counter
(integer) 101
> incrby counter 50
(integer) 151
> type counter
(integer)
```

### <a name="adding-an-expiration-time-to-values"></a><span data-ttu-id="fedbf-175">将过期时间添加到值</span><span class="sxs-lookup"><span data-stu-id="fedbf-175">Adding an expiration time to values</span></span>

<span data-ttu-id="fedbf-176">缓存非常重要, 因为它允许我们将常用值存储在内存中。</span><span class="sxs-lookup"><span data-stu-id="fedbf-176">Caching is important because it allows us to store commonly used values in memory.</span></span> <span data-ttu-id="fedbf-177">但是, 我们还需要一种在值过时时过期值的方法。</span><span class="sxs-lookup"><span data-stu-id="fedbf-177">However, we also need a way to expire values when they are stale.</span></span> <span data-ttu-id="fedbf-178">在 Redis 中, 通过将_时间生存时间_(TTL) 应用到某个键来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="fedbf-178">In Redis this is done by applying a _time to live_ (TTL) to a key.</span></span>

<span data-ttu-id="fedbf-179">当 TTL 过期时, 将自动删除密钥, 就像发出 DEL 命令一样。</span><span class="sxs-lookup"><span data-stu-id="fedbf-179">When the TTL elapses, the key is automatically deleted, exactly as if the DEL command were issued.</span></span> <span data-ttu-id="fedbf-180">下面是有关 TTL 到期的一些注意事项。</span><span class="sxs-lookup"><span data-stu-id="fedbf-180">Here are some notes on TTL expirations.</span></span>

- <span data-ttu-id="fedbf-181">可以使用秒或毫秒精度设置过期时间。</span><span class="sxs-lookup"><span data-stu-id="fedbf-181">Expirations can be set using seconds or milliseconds precision.</span></span>
- <span data-ttu-id="fedbf-182">过期时间解析始终为1毫秒。</span><span class="sxs-lookup"><span data-stu-id="fedbf-182">The expire time resolution is always 1 millisecond.</span></span>
- <span data-ttu-id="fedbf-183">有关过期的信息会复制并保存在磁盘上, 当 Redis 服务器保持停止时, 几乎会通过此时间传递 (这意味着 Redis 将保存密钥过期的日期)。</span><span class="sxs-lookup"><span data-stu-id="fedbf-183">Information about expires are replicated and persisted on disk, the time virtually passes when your Redis server remains stopped (this means that Redis saves the date at which a key will expire).</span></span>

<span data-ttu-id="fedbf-184">下面是一个过期的示例:</span><span class="sxs-lookup"><span data-stu-id="fedbf-184">Here is an example of an expiration:</span></span>

```output
> set counter 100
OK
> expire counter 5
(integer) 1
> get counter
100
... wait ...
> get counter
(nil)
```

## <a name="accessing-a-redis-cache-from-a-client"></a><span data-ttu-id="fedbf-185">从客户端访问 Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="fedbf-185">Accessing a Redis cache from a client</span></span>

<span data-ttu-id="fedbf-186">若要连接到 Redis 实例的 Azure 缓存, 需要多条信息。</span><span class="sxs-lookup"><span data-stu-id="fedbf-186">To connect to an Azure Cache for Redis instance, you'll need several pieces of information.</span></span> <span data-ttu-id="fedbf-187">客户端需要缓存的主机名、端口和访问密钥。</span><span class="sxs-lookup"><span data-stu-id="fedbf-187">Clients need the host name, port, and an access key for the cache.</span></span> <span data-ttu-id="fedbf-188">您可以通过 "**设置 > 访问密钥**" 页面在 Azure 门户中检索此信息。</span><span class="sxs-lookup"><span data-stu-id="fedbf-188">You can retrieve this information in the Azure portal through the **Settings > Access Keys** page.</span></span> 

- <span data-ttu-id="fedbf-189">主机名是缓存的公共 Internet 地址, 它是使用缓存名称创建的。</span><span class="sxs-lookup"><span data-stu-id="fedbf-189">The host name is the public Internet address of your cache, which was created using the name of the cache.</span></span> <span data-ttu-id="fedbf-190">例如`sportsresults.redis.cache.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="fedbf-190">For example `sportsresults.redis.cache.windows.net`.</span></span>

- <span data-ttu-id="fedbf-191">访问键充当缓存的密码。</span><span class="sxs-lookup"><span data-stu-id="fedbf-191">The access key acts as a password for your cache.</span></span> <span data-ttu-id="fedbf-192">创建了两个键: 主和辅助。</span><span class="sxs-lookup"><span data-stu-id="fedbf-192">There are two keys created: primary and secondary.</span></span> <span data-ttu-id="fedbf-193">您可以使用两个键中的任意一个, 以在需要更改主键的情况下提供。</span><span class="sxs-lookup"><span data-stu-id="fedbf-193">You can use either key, two are provided in case you need to change the primary key.</span></span> <span data-ttu-id="fedbf-194">您可以将所有客户端切换到辅助密钥, 然后重新生成主键。</span><span class="sxs-lookup"><span data-stu-id="fedbf-194">You can switch all of your clients to the secondary key, and regenerate the primary key.</span></span> <span data-ttu-id="fedbf-195">这将阻止使用原始主关键字的任何应用程序。</span><span class="sxs-lookup"><span data-stu-id="fedbf-195">This would block any applications using the original primary key.</span></span> <span data-ttu-id="fedbf-196">Microsoft 建议定期重新生成密钥, 就像你的个人密码一样。</span><span class="sxs-lookup"><span data-stu-id="fedbf-196">Microsoft recommends periodically regenerating the keys - much like you would your personal passwords.</span></span>

> [!WARNING]
> <span data-ttu-id="fedbf-197">你的访问密钥应被视为机密信息, 请像对待密码那样对待。</span><span class="sxs-lookup"><span data-stu-id="fedbf-197">Your access keys should be considered confidential information, treat them like you would a password.</span></span> <span data-ttu-id="fedbf-198">拥有访问密钥的任何人都可以在缓存上执行任何操作!</span><span class="sxs-lookup"><span data-stu-id="fedbf-198">Anyone who has an access key can perform any operation on your cache!</span></span>
