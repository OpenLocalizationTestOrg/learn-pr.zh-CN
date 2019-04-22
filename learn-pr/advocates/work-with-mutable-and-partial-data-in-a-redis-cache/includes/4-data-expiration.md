<span data-ttu-id="a91fe-101">数据并非始终是永久性的, 有时您想要将其在特定时间删除。</span><span class="sxs-lookup"><span data-stu-id="a91fe-101">Data is not always permanent, and there are times you would like to delete it at a specific time.</span></span> <span data-ttu-id="a91fe-102">例如, 在即时消息应用程序中, 用户可以设置组聊天的显示名称。</span><span class="sxs-lookup"><span data-stu-id="a91fe-102">For example, in your instant messaging application, users can set the display name of the group chat.</span></span> <span data-ttu-id="a91fe-103">但是, 您希望名称在一小时后重置。</span><span class="sxs-lookup"><span data-stu-id="a91fe-103">However, you want the name to reset after one hour.</span></span> <span data-ttu-id="a91fe-104">为此, 您可以编写自己的服务器端逻辑来设置小时计时器并删除名称。</span><span class="sxs-lookup"><span data-stu-id="a91fe-104">You could accomplish this by writing your own server-side logic that set an hour timer and deleted the name.</span></span> <span data-ttu-id="a91fe-105">但是, Redis 的 Azure 缓存支持数据过期, 这是一项功能, 可以自动执行此功能, 而无需编写额外的逻辑。</span><span class="sxs-lookup"><span data-stu-id="a91fe-105">However, Azure Cache for Redis supports data expiration, which is a feature that does this automatically without writing additional logic.</span></span>

<span data-ttu-id="a91fe-106">在这里, 你将了解用于实现数据过期的常见 Redis 命令。</span><span class="sxs-lookup"><span data-stu-id="a91fe-106">Here, you'll learn about the common Redis commands to implement data expiration.</span></span>

## <a name="what-is-data-expiration"></a><span data-ttu-id="a91fe-107">什么是数据过期？</span><span class="sxs-lookup"><span data-stu-id="a91fe-107">What is data expiration?</span></span>

<span data-ttu-id="a91fe-108">数据过期是一项功能, 可在设定的一段时间后自动删除缓存中的密钥和值。</span><span class="sxs-lookup"><span data-stu-id="a91fe-108">Data expiration is a feature that can automatically delete a key and value in the cache after a set amount of time.</span></span>

## <a name="why-use-data-expiration"></a><span data-ttu-id="a91fe-109">为什么要使用数据过期？</span><span class="sxs-lookup"><span data-stu-id="a91fe-109">Why use data expiration?</span></span>

<span data-ttu-id="a91fe-110">数据过期通常在存储数据的生存期较短的情况下使用。</span><span class="sxs-lookup"><span data-stu-id="a91fe-110">Data expiration is commonly used in situations where the data you're storing is short-lived.</span></span>  <span data-ttu-id="a91fe-111">这一点很重要, 因为 Redis 的 Azure 缓存是内存中的数据库, 并且您没有足够的内存可供您使用, 如存储在磁盘上。</span><span class="sxs-lookup"><span data-stu-id="a91fe-111">This is important because Azure Cache for Redis is an in-memory database and you don't have as much memory available to use as you would if you were storing on disk.</span></span> <span data-ttu-id="a91fe-112">由于具有 Redis 的 Azure 缓存的存储空间有限, 因此您需要确保仅存储重要数据。</span><span class="sxs-lookup"><span data-stu-id="a91fe-112">Since you have limited storage with Azure Cache for Redis, you want to make sure you're only storing data that is important.</span></span> <span data-ttu-id="a91fe-113">如果数据不需要很长一段时间, 请确保设置了过期时间。</span><span class="sxs-lookup"><span data-stu-id="a91fe-113">If the data doesn't need to be around for a long time, make sure you set an expiration.</span></span>

## <a name="how-to-use-data-expiration-in-azure-cache-for-redis"></a><span data-ttu-id="a91fe-114">如何在 Redis 中使用 Azure 缓存中的数据过期</span><span class="sxs-lookup"><span data-stu-id="a91fe-114">How to use data expiration in Azure Cache for Redis</span></span>

<span data-ttu-id="a91fe-115">在 Redis 的 Azure 缓存中实施和管理数据过期的命令有不同之处:</span><span class="sxs-lookup"><span data-stu-id="a91fe-115">There are different commands to implement and manage data expiration in Azure Cache for Redis:</span></span>

- <span data-ttu-id="a91fe-116">`EXPIRE`: 设置一个密钥的超时值 (以秒为单位)</span><span class="sxs-lookup"><span data-stu-id="a91fe-116">`EXPIRE`: Sets the timeout of a key in seconds</span></span>
- <span data-ttu-id="a91fe-117">`PEXPIRE`: 设置密钥的超时值 (以毫秒为单位)</span><span class="sxs-lookup"><span data-stu-id="a91fe-117">`PEXPIRE`: Sets the timeout of a key in milliseconds</span></span>
- <span data-ttu-id="a91fe-118">`EXPIREAT`: 使用绝对 Unix 时间戳 (以秒为单位) 设置键的超时值</span><span class="sxs-lookup"><span data-stu-id="a91fe-118">`EXPIREAT`: Sets the timeout of a key using an absolute Unix timestamp in seconds</span></span>
- <span data-ttu-id="a91fe-119">`PEXPIREAT`: 使用绝对 Unix 时间戳 (以毫秒为单位) 设置密钥的超时值</span><span class="sxs-lookup"><span data-stu-id="a91fe-119">`PEXPIREAT`: Sets the timeout of a key using an absolute Unix timestamp in milliseconds</span></span>
- <span data-ttu-id="a91fe-120">`TTL`: 返回密钥必须在几秒内生存的剩余时间</span><span class="sxs-lookup"><span data-stu-id="a91fe-120">`TTL`: Returns the remaining time a key has to live in seconds</span></span>
- <span data-ttu-id="a91fe-121">`PTTL`: 返回键必须以毫秒为单位生存的剩余时间</span><span class="sxs-lookup"><span data-stu-id="a91fe-121">`PTTL`: Returns the remaining time a key has to live in milliseconds</span></span>
- <span data-ttu-id="a91fe-122">`PERSIST`: 使密钥永不过期</span><span class="sxs-lookup"><span data-stu-id="a91fe-122">`PERSIST`: Makes a key never expire</span></span>

<span data-ttu-id="a91fe-123">最常见的命令是`EXPIRE`, 我们将在整个模块中使用它。</span><span class="sxs-lookup"><span data-stu-id="a91fe-123">The most common command is `EXPIRE`, and we'll use it throughout this module.</span></span>

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a><span data-ttu-id="a91fe-124">使用 c # 和 ServiceStack 的数据过期示例 Redis</span><span class="sxs-lookup"><span data-stu-id="a91fe-124">Example of data expiration using C# and ServiceStack.Redis</span></span>

<span data-ttu-id="a91fe-125">请记住, 在使用客户端库 (如**ServiceStack**) 时, 我们不必担心为 Redis 命令记住低级别 Azure 缓存。</span><span class="sxs-lookup"><span data-stu-id="a91fe-125">Remember, when using a client library like **ServiceStack.Redis**, we don't have to worry about remembering the low-level Azure Cache for Redis commands.</span></span> <span data-ttu-id="a91fe-126">相反, 我们可以使用简单的 c # 方法。</span><span class="sxs-lookup"><span data-stu-id="a91fe-126">Instead, we can use simple C# methods.</span></span>

```csharp
public static void SetGroupChatName(string groupChatID, string chatName)
{
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create a key for group chat display names
        string key = groupChatID + "displayName";

        //Set the group chat display name
        redisClient.SetValue(key, chatName);

        //Set the expiration for one hour
        redisClient.Expire(key, 3600);
    }
}
```

<span data-ttu-id="a91fe-127">Redis 的 Azure 缓存允许您在经过一段时间后使用数据过期来自动删除数据。</span><span class="sxs-lookup"><span data-stu-id="a91fe-127">Azure Cache for Redis allows you to delete data automatically after a set amount of time using data expiration.</span></span> <span data-ttu-id="a91fe-128">这一点很重要, 因为 Redis 的 Azure 缓存是内存中的数据库, 并且您没有像将数据存储在磁盘上那样多的可用内存。</span><span class="sxs-lookup"><span data-stu-id="a91fe-128">This is important because Azure Cache for Redis is an in-memory database, and you don't have as much memory available as you would with storing data on disk.</span></span> <span data-ttu-id="a91fe-129">如果要存储的数据不需要很长时间, 请确保设置了一个过期时间。</span><span class="sxs-lookup"><span data-stu-id="a91fe-129">If the data you're storing doesn't need to be around for a long time, make sure you set an expiration.</span></span>