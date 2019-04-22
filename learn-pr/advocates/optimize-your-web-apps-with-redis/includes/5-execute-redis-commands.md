<span data-ttu-id="a6948-101">如前所述, Redis 是内存中的 NoSQL 数据库, 可在多个服务器之间复制。</span><span class="sxs-lookup"><span data-stu-id="a6948-101">As mentioned earlier, Redis is an in-memory NoSQL database which can be replicated across multiple servers.</span></span> <span data-ttu-id="a6948-102">它通常用作缓存, 但可用作正式的数据库或甚至是消息代理。</span><span class="sxs-lookup"><span data-stu-id="a6948-102">It is often used as a cache, but can be used as a formal database or even message-broker.</span></span> 

<span data-ttu-id="a6948-103">它可以存储各种数据类型和结构, 并支持可以发出的各种命令来检索缓存本身的缓存数据或查询信息。</span><span class="sxs-lookup"><span data-stu-id="a6948-103">It can store a variety of data types and structures and supports a variety of commands you can issue to retrieve cached data or query information about the cache itself.</span></span> <span data-ttu-id="a6948-104">您使用的数据始终存储为键/值对。</span><span class="sxs-lookup"><span data-stu-id="a6948-104">The data you work with is always stored as key/value pairs.</span></span>

## <a name="executing-commands-on-the-redis-cache"></a><span data-ttu-id="a6948-105">在 Redis 缓存上执行命令</span><span class="sxs-lookup"><span data-stu-id="a6948-105">Executing commands on the Redis cache</span></span>

<span data-ttu-id="a6948-106">通常情况下, 客户端应用程序将使用_客户端库_来表单请求并在 Redis 缓存上执行命令。</span><span class="sxs-lookup"><span data-stu-id="a6948-106">Typically, a client application will use a _client library_ to form requests and execute commands on a Redis cache.</span></span> <span data-ttu-id="a6948-107">您可以从[Redis 客户端页](https://redis.io/clients)中直接获取客户端库的列表。</span><span class="sxs-lookup"><span data-stu-id="a6948-107">You can get a list of client libraries directly from the [Redis clients page](https://redis.io/clients).</span></span> <span data-ttu-id="a6948-108">.net 语言的常见高性能 Redis 客户端是**StackExchange**。</span><span class="sxs-lookup"><span data-stu-id="a6948-108">A popular high-performance Redis client for the .NET language is **StackExchange.Redis**.</span></span> <span data-ttu-id="a6948-109">该包可通过 NuGet 使用, 并且可以使用命令行或 IDE 将其添加到 .net 代码中。</span><span class="sxs-lookup"><span data-stu-id="a6948-109">The package is available through NuGet and can be added to your .NET code using the command line or IDE.</span></span>

### <a name="connecting-to-your-redis-cache-with-stackexchangeredis"></a><span data-ttu-id="a6948-110">使用 StackExchange 连接到 Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="a6948-110">Connecting to your Redis cache with StackExchange.Redis</span></span>

<span data-ttu-id="a6948-111">请记住, 我们使用主机地址、端口号和访问密钥连接到 Redis 服务器。</span><span class="sxs-lookup"><span data-stu-id="a6948-111">Recall that we use the host address, port number, and an access key to connect to a Redis server.</span></span> <span data-ttu-id="a6948-112">Azure 还提供了一些 Redis 客户端的_连接字符串_, 这些客户端将此数据捆绑在一起组成一个字符串。</span><span class="sxs-lookup"><span data-stu-id="a6948-112">Azure also offers a _connection string_ for some Redis clients which bundles this data together into a single string.</span></span>

### <a name="what-is-a-connection-string"></a><span data-ttu-id="a6948-113">连接字符串是什么？</span><span class="sxs-lookup"><span data-stu-id="a6948-113">What is a connection string?</span></span>

<span data-ttu-id="a6948-114">连接字符串是单行文本, 包括要连接到 Azure 中的 Redis 缓存的所有必需的信息, 并进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a6948-114">A connection string is a single line of text that includes all the required pieces of information to connect and authenticate to a Redis cache in Azure.</span></span> <span data-ttu-id="a6948-115">它的外观如下所示 (**缓存名称**和**密码**字段以实际值填充):</span><span class="sxs-lookup"><span data-stu-id="a6948-115">It will look something like the following (with the **cache-name** and **password-here** fields filled in with real values):</span></span>

```
[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False
```

> [!TIP]
> <span data-ttu-id="a6948-116">应在应用程序中保护连接字符串。</span><span class="sxs-lookup"><span data-stu-id="a6948-116">The connection string should be protected in your application.</span></span> <span data-ttu-id="a6948-117">如果应用程序托管在 Azure 上, 请考虑使用 azure Key Vault 存储该值。</span><span class="sxs-lookup"><span data-stu-id="a6948-117">If the application is hosted on Azure, consider using an Azure Key Vault to store the value.</span></span>

<span data-ttu-id="a6948-118">您可以将此字符串传递给**StackExchange** , 以创建与服务器的连接。</span><span class="sxs-lookup"><span data-stu-id="a6948-118">You can pass this string to **StackExchange.Redis** to create a connection the server.</span></span> 

<span data-ttu-id="a6948-119">请注意, 末尾有两个其他参数:</span><span class="sxs-lookup"><span data-stu-id="a6948-119">Notice that there are two additional parameters at the end:</span></span> 

- <span data-ttu-id="a6948-120">**ssl** -确保通信的加密。</span><span class="sxs-lookup"><span data-stu-id="a6948-120">**ssl** - ensures that communication is encrypted.</span></span>
- <span data-ttu-id="a6948-121">**abortConnection** -即使当时服务器不可用, 也允许创建连接。</span><span class="sxs-lookup"><span data-stu-id="a6948-121">**abortConnection** - allows a connection to be created even if the server is unavailable at that moment.</span></span>

<span data-ttu-id="a6948-122">有几个其他[可选参数](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options)可以追加到字符串以配置客户端库。</span><span class="sxs-lookup"><span data-stu-id="a6948-122">There are several other [optional parameters](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options) you can append to the string to configure the client library.</span></span>

### <a name="creating-a-connection"></a><span data-ttu-id="a6948-123">创建连接</span><span class="sxs-lookup"><span data-stu-id="a6948-123">Creating a connection</span></span>

<span data-ttu-id="a6948-124">**StackExchange**中的 main connection 对象是`StackExchange.Redis.ConnectionMultiplexer`类。</span><span class="sxs-lookup"><span data-stu-id="a6948-124">The main connection object in **StackExchange.Redis** is the `StackExchange.Redis.ConnectionMultiplexer` class.</span></span> <span data-ttu-id="a6948-125">此对象将摘要连接到 Redis 服务器 (或服务器组) 的过程。</span><span class="sxs-lookup"><span data-stu-id="a6948-125">This object abstracts the process of connecting to a Redis server (or group of servers).</span></span> <span data-ttu-id="a6948-126">它经过优化, 可在需要访问缓存的情况下有效地管理连接并将其保留在周围。</span><span class="sxs-lookup"><span data-stu-id="a6948-126">It's optimized to manage connections efficiently and intended to be kept around while you need access to the cache.</span></span>

<span data-ttu-id="a6948-127">您可以使用`ConnectionMultiplexer`静态`ConnectionMultiplexer.Connect`或`ConnectionMultiplexer.ConnectAsync`方法创建一个实例, 传入一个连接字符串或一个`ConfigurationOptions`对象。</span><span class="sxs-lookup"><span data-stu-id="a6948-127">You create a `ConnectionMultiplexer` instance using the static `ConnectionMultiplexer.Connect` or `ConnectionMultiplexer.ConnectAsync` method, passing in either a connection string or a `ConfigurationOptions` object.</span></span> 

<span data-ttu-id="a6948-128">下面是一个简单的示例:</span><span class="sxs-lookup"><span data-stu-id="a6948-128">Here's a simple example:</span></span>

```csharp
using StackExchange.Redis;
...
var connectionString = "[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False";
var redisConnection = ConnectionMultiplexer.Connect(connectionString);
    // ^^^ store and re-use this!!!
```

<span data-ttu-id="a6948-129">拥有后`ConnectionMultiplexer`, 您可能需要执行3个主要操作:</span><span class="sxs-lookup"><span data-stu-id="a6948-129">Once you have a `ConnectionMultiplexer`, there are 3 primary things you might want to do:</span></span>

1. <span data-ttu-id="a6948-130">访问 Redis 数据库。</span><span class="sxs-lookup"><span data-stu-id="a6948-130">Access a Redis Database.</span></span> <span data-ttu-id="a6948-131">这正是我们将重点放在这里的。</span><span class="sxs-lookup"><span data-stu-id="a6948-131">This is what we will focus on here.</span></span>
2. <span data-ttu-id="a6948-132">使用 Redis 的发布者/下标功能。</span><span class="sxs-lookup"><span data-stu-id="a6948-132">Make use of the publisher/subscript features of Redis.</span></span> <span data-ttu-id="a6948-133">这超出了本模块的范围。</span><span class="sxs-lookup"><span data-stu-id="a6948-133">This is outside the scope of this module.</span></span>
3. <span data-ttu-id="a6948-134">出于维护或监视目的访问单个服务器。</span><span class="sxs-lookup"><span data-stu-id="a6948-134">Access an individual server for maintenance or monitoring purposes.</span></span>

### <a name="accessing-a-redis-database"></a><span data-ttu-id="a6948-135">访问 Redis 数据库</span><span class="sxs-lookup"><span data-stu-id="a6948-135">Accessing a Redis database</span></span>

<span data-ttu-id="a6948-136">Redis 数据库由`IDatabase`类型表示。</span><span class="sxs-lookup"><span data-stu-id="a6948-136">The Redis database is represented by the `IDatabase` type.</span></span> <span data-ttu-id="a6948-137">您可以使用`GetDatabase()`方法检索一个:</span><span class="sxs-lookup"><span data-stu-id="a6948-137">You can retrieve one using the `GetDatabase()` method:</span></span>

```csharp
IDatabase db = redisConnection.GetDatabase();
```

> [!TIP]
> <span data-ttu-id="a6948-138">从`GetDatabase`返回的对象是一个轻量对象, 不需要存储。</span><span class="sxs-lookup"><span data-stu-id="a6948-138">The object returned from `GetDatabase` is a lightweight object, and does not need to be stored.</span></span> <span data-ttu-id="a6948-139">仅`ConnectionMultiplexer`需要保持活动状态。</span><span class="sxs-lookup"><span data-stu-id="a6948-139">Only the `ConnectionMultiplexer` needs to be kept alive.</span></span>

<span data-ttu-id="a6948-140">拥有`IDatabase`对象后, 您可以执行方法以与缓存进行交互。</span><span class="sxs-lookup"><span data-stu-id="a6948-140">Once you have a `IDatabase` object, you can execute methods to interact with the cache.</span></span> <span data-ttu-id="a6948-141">所有方法都具有同步和异步版本, `Task`这将返回对象以使其`async`与`await`和关键字兼容。</span><span class="sxs-lookup"><span data-stu-id="a6948-141">All methods have synchronous and asynchronous versions which return `Task` objects to make them compatible with the `async` and `await` keywords.</span></span>

<span data-ttu-id="a6948-142">下面的示例展示了如何在缓存中存储项/值:</span><span class="sxs-lookup"><span data-stu-id="a6948-142">Here is an example of storing a key/value in the cache:</span></span>

```csharp
bool wasSet = db.StringSet("favorite:flavor", "i-love-rocky-road");
```

<span data-ttu-id="a6948-143">该`StringSet`方法返回一个`bool`值, 该值指示是否已设置`true`() 或不`false`设置 ()。</span><span class="sxs-lookup"><span data-stu-id="a6948-143">The `StringSet` method returns a `bool` indicating whether the value was set (`true`) or not (`false`).</span></span> <span data-ttu-id="a6948-144">然后, 我们可以使用`StringGet`方法检索值:</span><span class="sxs-lookup"><span data-stu-id="a6948-144">We can then retrieve the value with the `StringGet` method:</span></span>

```csharp
string value = db.StringGet("favorite:flavor");
Console.WriteLine(value); // displays: ""i-love-rocky-road""
```

#### <a name="getting-and-setting-binary-values"></a><span data-ttu-id="a6948-145">获取和设置二进制值</span><span class="sxs-lookup"><span data-stu-id="a6948-145">Getting and Setting binary values</span></span>

<span data-ttu-id="a6948-146">请记住, Redis 的密钥和值是_二进制安全_的。</span><span class="sxs-lookup"><span data-stu-id="a6948-146">Recall that Redis keys and values are _binary safe_.</span></span> <span data-ttu-id="a6948-147">这些相同的方法可用于存储二进制数据。</span><span class="sxs-lookup"><span data-stu-id="a6948-147">These same methods can be used to store binary data.</span></span> <span data-ttu-id="a6948-148">有一些隐式转换运算符可用于`byte[]`类型, 以便您可以自然地处理数据:</span><span class="sxs-lookup"><span data-stu-id="a6948-148">There are implicit conversion operators to work with `byte[]` types so you can work with the data naturally:</span></span>

```csharp
byte[] key = ...;
byte[] value = ...;

db.StringSet(key, value);
```

```csharp
byte[] key = ...;
byte[] value = db.StringGet(key);
```

> [!TIP]
> <span data-ttu-id="a6948-149">**StackExchange**使用`RedisKey`类型表示键。</span><span class="sxs-lookup"><span data-stu-id="a6948-149">**StackExchange.Redis** represents keys using the `RedisKey` type.</span></span> <span data-ttu-id="a6948-150">此类具有与`string`和`byte[]`的隐式转换, 同时允许使用文本和二进制密钥而不会出现任何复杂的情况。</span><span class="sxs-lookup"><span data-stu-id="a6948-150">This class has implicit conversions to and from both `string` and `byte[]`, allowing both text and binary keys to be used without any complication.</span></span> <span data-ttu-id="a6948-151">值由`RedisValue`类型表示。</span><span class="sxs-lookup"><span data-stu-id="a6948-151">Values are represented by the `RedisValue` type.</span></span> <span data-ttu-id="a6948-152">与一起`RedisKey`使用时, 存在适当的隐式转换, 可以让`string`您`byte[]`传递或。</span><span class="sxs-lookup"><span data-stu-id="a6948-152">As with `RedisKey`, there are implicit conversions in place to allow you to pass `string` or `byte[]`.</span></span>

#### <a name="other-common-operations"></a><span data-ttu-id="a6948-153">其他常见操作</span><span class="sxs-lookup"><span data-stu-id="a6948-153">Other common operations</span></span>

<span data-ttu-id="a6948-154">该`IDatabase`接口包括其他几种使用 Redis 缓存的方法。</span><span class="sxs-lookup"><span data-stu-id="a6948-154">The `IDatabase` interface includes several other methods to work with the Redis cache.</span></span> <span data-ttu-id="a6948-155">有一些方法可以使用哈希、列表、集和排序集。</span><span class="sxs-lookup"><span data-stu-id="a6948-155">There are methods to work with hashes, lists, sets, and ordered sets.</span></span>

<span data-ttu-id="a6948-156">下面是使用单个密钥的一些较常见的代码, 可以读取接口的[源代码](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs)以查看完整列表。</span><span class="sxs-lookup"><span data-stu-id="a6948-156">Here are some of the more common ones that work with single keys, you can [read the source code](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs) for the interface to see the full list.</span></span>

| <span data-ttu-id="a6948-157">方法</span><span class="sxs-lookup"><span data-stu-id="a6948-157">Method</span></span> | <span data-ttu-id="a6948-158">说明</span><span class="sxs-lookup"><span data-stu-id="a6948-158">Description</span></span> |
|--------|-------------|
| `CreateBatch` | <span data-ttu-id="a6948-159">创建一_组_将作为单个单元发送到服务器但不一定作为一个单元进行处理的操作。</span><span class="sxs-lookup"><span data-stu-id="a6948-159">Creates a _group of operations_ that will be sent to the server as a single unit, but not necessarily processed as a unit.</span></span> |
| `CreateTransaction` | <span data-ttu-id="a6948-160">创建一组将作为单个单元发送到服务器_并_在服务器上作为一个单元进行处理的操作。</span><span class="sxs-lookup"><span data-stu-id="a6948-160">Creates a group of operations that will be sent to the server as a single unit _and_ processed on the server as a single unit.</span></span> |
| `KeyDelete` | <span data-ttu-id="a6948-161">删除键/值。</span><span class="sxs-lookup"><span data-stu-id="a6948-161">Delete the key/value.</span></span> |
| `KeyExists` | <span data-ttu-id="a6948-162">返回给定的键是否存在于缓存中。</span><span class="sxs-lookup"><span data-stu-id="a6948-162">Returns whether the given key exists in cache.</span></span> |
| `KeyExpire` | <span data-ttu-id="a6948-163">在项上设置生存时间 (TTL) 过期时间。</span><span class="sxs-lookup"><span data-stu-id="a6948-163">Sets a time-to-live (TTL) expiration on a key.</span></span> |
| `KeyRename` | <span data-ttu-id="a6948-164">重命名密钥。</span><span class="sxs-lookup"><span data-stu-id="a6948-164">Renames a key.</span></span> |
| `KeyTimeToLive` | <span data-ttu-id="a6948-165">返回键的 TTL。</span><span class="sxs-lookup"><span data-stu-id="a6948-165">Returns the TTL for a key.</span></span> |
| `KeyType` | <span data-ttu-id="a6948-166">返回存储在键上的值的类型的字符串表示形式。</span><span class="sxs-lookup"><span data-stu-id="a6948-166">Returns the string representation of the type of the value stored at key.</span></span> <span data-ttu-id="a6948-167">可返回的不同类型为: string、list、set、zset 和 hash。</span><span class="sxs-lookup"><span data-stu-id="a6948-167">The different types that can be returned are: string, list, set, zset and hash.</span></span> |
       
### <a name="executing-other-commands"></a><span data-ttu-id="a6948-168">执行其他命令</span><span class="sxs-lookup"><span data-stu-id="a6948-168">Executing other commands</span></span>

<span data-ttu-id="a6948-169">`IDatabase`对象具有`Execute`和`ExecuteAsync`方法, 可用于将文本命令传递给 Redis 服务器。</span><span class="sxs-lookup"><span data-stu-id="a6948-169">The `IDatabase` object has an `Execute` and `ExecuteAsync` method which can be used to pass textual commands to the Redis server.</span></span> <span data-ttu-id="a6948-170">例如：</span><span class="sxs-lookup"><span data-stu-id="a6948-170">For example:</span></span>

```csharp
var result = db.Execute("ping");
Console.WriteLine(result.ToString()); // displays: "PONG"
```

<span data-ttu-id="a6948-171">和方法返回一个包含`RedisResult`以下两个属性的数据持有者的对象: `ExecuteAsync` `Execute`</span><span class="sxs-lookup"><span data-stu-id="a6948-171">The `Execute` and `ExecuteAsync` methods return a `RedisResult` object which is a data holder that includes two properties:</span></span>

- <span data-ttu-id="a6948-172">`Type`这将返回`string`指示结果的类型-"STRING"、"INTEGER" 等的类型。</span><span class="sxs-lookup"><span data-stu-id="a6948-172">`Type` which returns a `string` indicating the type of the result - "STRING", "INTEGER", etc.</span></span>
- <span data-ttu-id="a6948-173">`IsNull`要在结果为`null`时检测到的 true/false 值。</span><span class="sxs-lookup"><span data-stu-id="a6948-173">`IsNull` a true/false value to detect when the result is `null`.</span></span>

<span data-ttu-id="a6948-174">然后, 可以在`ToString()`上使用`RedisResult`来获取实际返回值。</span><span class="sxs-lookup"><span data-stu-id="a6948-174">You can then use `ToString()` on the `RedisResult` to get the actual return value.</span></span>

<span data-ttu-id="a6948-175">您可以使用`Execute`执行任何支持的命令-例如, 我们可以获取连接到缓存的所有客户端 ("客户端列表"):</span><span class="sxs-lookup"><span data-stu-id="a6948-175">You can use `Execute` to perform any supported commands - for example, we can get all the clients connected to the cache ("CLIENT LIST"):</span></span>

```csharp
var result = await db.ExecuteAsync("client", "list");
Console.WriteLine($"Type = {result.Type}\r\nResult = {result}");
```

<span data-ttu-id="a6948-176">这将输出所有连接的客户端:</span><span class="sxs-lookup"><span data-stu-id="a6948-176">This would output all the connected clients:</span></span>

```output
Type = BulkString
Result = id=9469 addr=16.183.122.154:54961 fd=18 name=DESKTOP-AAAAAA age=0 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=subscribe numops=5
id=9470 addr=16.183.122.155:54967 fd=13 name=DESKTOP-BBBBBB age=0 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=client numops=17
```

### <a name="storing-more-complex-values"></a><span data-ttu-id="a6948-177">存储更复杂的值</span><span class="sxs-lookup"><span data-stu-id="a6948-177">Storing more complex values</span></span>
<span data-ttu-id="a6948-178">Redis 面向二进制安全字符串, 但您可以通过将它们序列化为文本格式 (通常为 XML 或 JSON) 来缓冲对象图。</span><span class="sxs-lookup"><span data-stu-id="a6948-178">Redis is oriented around binary safe strings, but you can cache off object graphs by serializing them to a textual format - typically XML or JSON.</span></span> <span data-ttu-id="a6948-179">例如, 对于我们的统计信息, 我们有一个`GameStats`如下所示的对象:</span><span class="sxs-lookup"><span data-stu-id="a6948-179">For example, perhaps for our statistics, we have a `GameStats` object which looks like:</span></span>

```csharp
public class GameStat
{
    public string Id { get; set; }
    public string Sport { get; set; }
    public DateTimeOffset DatePlayed { get; set; }
    public string Game { get; set; }
    public IReadOnlyList<string> Teams { get; set; }
    public IReadOnlyList<(string team, int score)> Results { get; set; }

    public GameStat(string sport, DateTimeOffset datePlayed, string game, string[] teams, IEnumerable<(string team, int score)> results)
    {
        Id = Guid.NewGuid().ToString();
        Sport = sport;
        DatePlayed = datePlayed;
        Game = game;
        Teams = teams.ToList();
        Results = results.ToList();
    }

    public override string ToString()
    {
        return $"{Sport} {Game} played on {DatePlayed.Date.ToShortDateString()} - " +
               $"{String.Join(',', Teams)}\r\n\t" + 
               $"{String.Join('\t', Results.Select(r => $"{r.team } - {r.score}\r\n"))}";
    }
}
```

<span data-ttu-id="a6948-180">我们可以使用**newtonsoft.json**库将此对象的实例转换为字符串:</span><span class="sxs-lookup"><span data-stu-id="a6948-180">We could use the **Newtonsoft.Json** library to turn an instance of this object into a string:</span></span>

```csharp
var stat = new GameStat("Soccer", new DateTime(1950, 7, 16), "FIFA World Cup", 
                new[] { "Uruguay", "Brazil" },
                new[] { ("Uruguay", 2), ("Brazil", 1) });

string serializedValue = Newtonsoft.Json.JsonConvert.SerializeObject(stat);
bool added = db.StringSet("event:1950-world-cup", serializedValue);
```

<span data-ttu-id="a6948-181">我们可以检索它, 并使用反向进程将其转换回对象:</span><span class="sxs-lookup"><span data-stu-id="a6948-181">We could retrieve it and turn it back into an object using the reverse process:</span></span>

```csharp
var result = db.StringGet("event:1950-world-cup");
var stat = Newtonsoft.Json.JsonConvert.DeserializeObject<GameStat>(result.ToString());
Console.WriteLine(stat.Sport); // displays "Soccer"
```

## <a name="cleaning-up-the-connection"></a><span data-ttu-id="a6948-182">清理连接</span><span class="sxs-lookup"><span data-stu-id="a6948-182">Cleaning up the connection</span></span>
<span data-ttu-id="a6948-183">完成 Redis 连接后, 即可**释放** `ConnectionMultiplexer`。</span><span class="sxs-lookup"><span data-stu-id="a6948-183">Once you are done with the Redis connection, you can **Dispose** the `ConnectionMultiplexer`.</span></span> <span data-ttu-id="a6948-184">这将关闭所有连接并关闭与服务器的通信。</span><span class="sxs-lookup"><span data-stu-id="a6948-184">This will close all connections and shutdown the communication to the server.</span></span>

```csharp
redisConnection.Dispose();
redisConnection = null;
```

<span data-ttu-id="a6948-185">让我们创建一个应用程序, 并使用我们的 Redis 缓存进行一些简单的操作。</span><span class="sxs-lookup"><span data-stu-id="a6948-185">Let's create an application and do some simple work with our Redis cache.</span></span>