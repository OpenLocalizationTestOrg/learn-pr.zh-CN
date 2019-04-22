<span data-ttu-id="424dc-101">对于 Redis 的 Azure 缓存而言, 内存是最关键的资源, 因为它是内存中的数据库。</span><span class="sxs-lookup"><span data-stu-id="424dc-101">Memory is the most critical resource for Azure Cache for Redis, because it's an in-memory database.</span></span> <span data-ttu-id="424dc-102">当您开始添加超过可用内存量的数据时, 您可能会遇到问题。</span><span class="sxs-lookup"><span data-stu-id="424dc-102">You can run into problems when you begin adding data that exceeds the amount of memory available.</span></span> <span data-ttu-id="424dc-103">Redis 的 Azure 缓存支持逐出策略, 这些策略指示在内存不足时应如何处理数据。</span><span class="sxs-lookup"><span data-stu-id="424dc-103">Azure Cache for Redis supports eviction policies, which indicate how data should be handled when you run out of memory.</span></span>

<span data-ttu-id="424dc-104">在这里, 你将设置一个逐出策略, 以确定当超出最大内存量时, 您的数据应执行的操作。</span><span class="sxs-lookup"><span data-stu-id="424dc-104">Here, you'll set an eviction policy to determine what your data should do when you exceed the maximum amount of memory.</span></span>

## <a name="what-is-an-eviction-policy"></a><span data-ttu-id="424dc-105">什么是逐出策略？</span><span class="sxs-lookup"><span data-stu-id="424dc-105">What is an eviction policy?</span></span>

<span data-ttu-id="424dc-106">逐出策略是一种计划, 用于确定当超出可用的最大内存量时应如何管理数据。</span><span class="sxs-lookup"><span data-stu-id="424dc-106">An eviction policy is a plan that determines how your data should be managed when you exceed the maximum amount of memory available.</span></span> <span data-ttu-id="424dc-107">例如, 使用逐出策略, 可以告诉 Redis 的 Azure 缓存删除随机密钥, 为插入的新数据留出空间。</span><span class="sxs-lookup"><span data-stu-id="424dc-107">For example, using an eviction policy, you could tell Azure Cache for Redis to delete a random key to make room for the new data being inserted.</span></span>

### <a name="types-of-eviction-policies"></a><span data-ttu-id="424dc-108">逐出策略的类型</span><span class="sxs-lookup"><span data-stu-id="424dc-108">Types of eviction policies</span></span>

<span data-ttu-id="424dc-109">Azure Cache 为 Redis 提供了六种不同的逐出策略。</span><span class="sxs-lookup"><span data-stu-id="424dc-109">There are six different eviction policies provided by Azure Cache for Redis.</span></span> <span data-ttu-id="424dc-110">当您在内存不足时尝试插入数据时, 所有这些值都将执行操作。</span><span class="sxs-lookup"><span data-stu-id="424dc-110">All of these values perform an action when you attempt to insert data when you're out of memory.</span></span>

* <span data-ttu-id="424dc-111">**noeviction:** 无逐出策略。</span><span class="sxs-lookup"><span data-stu-id="424dc-111">**noeviction:** No eviction policy.</span></span> <span data-ttu-id="424dc-112">如果尝试插入数据, 则返回错误消息。</span><span class="sxs-lookup"><span data-stu-id="424dc-112">Returns an error message if you attempt to insert data.</span></span>

* <span data-ttu-id="424dc-113">**allkeys-lru:** 删除最近使用最少的键。</span><span class="sxs-lookup"><span data-stu-id="424dc-113">**allkeys-lru:** Removes the least recently used key.</span></span>

* <span data-ttu-id="424dc-114">**allkeys-随机:** 删除随机密钥。</span><span class="sxs-lookup"><span data-stu-id="424dc-114">**allkeys-random:** Removes a random key.</span></span>

* <span data-ttu-id="424dc-115">**可变-lru:** 从所有具有过期设置的键中删除最近使用最少的键。</span><span class="sxs-lookup"><span data-stu-id="424dc-115">**volatile-lru:** Removes the least recently used key out of all the keys with an expiration set.</span></span>

* <span data-ttu-id="424dc-116">**可变 ttl:** 根据它的过期设置, 删除最短生存时间的密钥。</span><span class="sxs-lookup"><span data-stu-id="424dc-116">**volatile-ttl:** Removes the key with the shortest time to live based on the expiration set for it.</span></span>

* <span data-ttu-id="424dc-117">**可变-随机:** 删除具有过期集的随机密钥。</span><span class="sxs-lookup"><span data-stu-id="424dc-117">**volatile-random:** Removes a random key that has an expiration set.</span></span>

## <a name="how-to-set-an-eviction-policy"></a><span data-ttu-id="424dc-118">如何设置逐出策略</span><span class="sxs-lookup"><span data-stu-id="424dc-118">How to set an eviction policy</span></span>

<span data-ttu-id="424dc-119">azure 提供了一个简单的下拉菜单, 可为 Redis 设置 Azure 缓存的逐出策略。</span><span class="sxs-lookup"><span data-stu-id="424dc-119">Azure provides a simple drop-down menu to set the eviction policy for Azure Cache for Redis.</span></span> <span data-ttu-id="424dc-120">选择 "**高级设置**", 然后使用 "maxmemory" 下拉菜单中的 "**策略**"。</span><span class="sxs-lookup"><span data-stu-id="424dc-120">Select **Advanced Settings**, and use the **maxmemory-policy** drop-down menu.</span></span>

<span data-ttu-id="424dc-121">由于内存对 Redis 的 Azure 缓存至关重要, 因此支持逐出策略。</span><span class="sxs-lookup"><span data-stu-id="424dc-121">Since memory is critical to Azure Cache for Redis, there is support for eviction policies.</span></span> <span data-ttu-id="424dc-122">逐出策略确定当内存不足并尝试插入新数据时, 对现有数据应执行的操作。</span><span class="sxs-lookup"><span data-stu-id="424dc-122">An eviction policy determines what should be done with existing data when you're out of memory and attempt to insert new data.</span></span>