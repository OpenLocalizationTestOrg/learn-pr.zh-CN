如前所述, Redis 是内存中的 NoSQL 数据库, 可在多个服务器之间复制。 它通常用作缓存, 但可用作正式的数据库或甚至是消息代理。 

它可以存储各种数据类型和结构, 并支持可以发出的各种命令来检索缓存本身的缓存数据或查询信息。 您使用的数据始终存储为键/值对。

## <a name="executing-commands-on-the-redis-cache"></a>在 Redis 缓存上执行命令

通常情况下, 客户端应用程序将使用_客户端库_来表单请求并在 Redis 缓存上执行命令。 您可以从[Redis 客户端页](https://redis.io/clients)中直接获取客户端库的列表。 .net 语言的常见高性能 Redis 客户端是**StackExchange**。 该包可通过 NuGet 使用, 并且可以使用命令行或 IDE 将其添加到 .net 代码中。

### <a name="connecting-to-your-redis-cache-with-stackexchangeredis"></a>使用 StackExchange 连接到 Redis 缓存

请记住, 我们使用主机地址、端口号和访问密钥连接到 Redis 服务器。 Azure 还提供了一些 Redis 客户端的_连接字符串_, 这些客户端将此数据捆绑在一起组成一个字符串。

### <a name="what-is-a-connection-string"></a>连接字符串是什么？

连接字符串是单行文本, 包括要连接到 Azure 中的 Redis 缓存的所有必需的信息, 并进行身份验证。 它的外观如下所示 (**缓存名称**和**密码**字段以实际值填充):

```
[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False
```

> [!TIP]
> 应在应用程序中保护连接字符串。 如果应用程序托管在 Azure 上, 请考虑使用 azure Key Vault 存储该值。

您可以将此字符串传递给**StackExchange** , 以创建与服务器的连接。 

请注意, 末尾有两个其他参数: 

- **ssl** -确保通信的加密。
- **abortConnection** -即使当时服务器不可用, 也允许创建连接。

有几个其他[可选参数](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options)可以追加到字符串以配置客户端库。

### <a name="creating-a-connection"></a>创建连接

**StackExchange**中的 main connection 对象是`StackExchange.Redis.ConnectionMultiplexer`类。 此对象将摘要连接到 Redis 服务器 (或服务器组) 的过程。 它经过优化, 可在需要访问缓存的情况下有效地管理连接并将其保留在周围。

您可以使用`ConnectionMultiplexer`静态`ConnectionMultiplexer.Connect`或`ConnectionMultiplexer.ConnectAsync`方法创建一个实例, 传入一个连接字符串或一个`ConfigurationOptions`对象。 

下面是一个简单的示例:

```csharp
using StackExchange.Redis;
...
var connectionString = "[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False";
var redisConnection = ConnectionMultiplexer.Connect(connectionString);
    // ^^^ store and re-use this!!!
```

拥有后`ConnectionMultiplexer`, 您可能需要执行3个主要操作:

1. 访问 Redis 数据库。 这正是我们将重点放在这里的。
2. 使用 Redis 的发布者/下标功能。 这超出了本模块的范围。
3. 出于维护或监视目的访问单个服务器。

### <a name="accessing-a-redis-database"></a>访问 Redis 数据库

Redis 数据库由`IDatabase`类型表示。 您可以使用`GetDatabase()`方法检索一个:

```csharp
IDatabase db = redisConnection.GetDatabase();
```

> [!TIP]
> 从`GetDatabase`返回的对象是一个轻量对象, 不需要存储。 仅`ConnectionMultiplexer`需要保持活动状态。

拥有`IDatabase`对象后, 您可以执行方法以与缓存进行交互。 所有方法都具有同步和异步版本, `Task`这将返回对象以使其`async`与`await`和关键字兼容。

下面的示例展示了如何在缓存中存储项/值:

```csharp
bool wasSet = db.StringSet("favorite:flavor", "i-love-rocky-road");
```

该`StringSet`方法返回一个`bool`值, 该值指示是否已设置`true`() 或不`false`设置 ()。 然后, 我们可以使用`StringGet`方法检索值:

```csharp
string value = db.StringGet("favorite:flavor");
Console.WriteLine(value); // displays: ""i-love-rocky-road""
```

#### <a name="getting-and-setting-binary-values"></a>获取和设置二进制值

请记住, Redis 的密钥和值是_二进制安全_的。 这些相同的方法可用于存储二进制数据。 有一些隐式转换运算符可用于`byte[]`类型, 以便您可以自然地处理数据:

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
> **StackExchange**使用`RedisKey`类型表示键。 此类具有与`string`和`byte[]`的隐式转换, 同时允许使用文本和二进制密钥而不会出现任何复杂的情况。 值由`RedisValue`类型表示。 与一起`RedisKey`使用时, 存在适当的隐式转换, 可以让`string`您`byte[]`传递或。

#### <a name="other-common-operations"></a>其他常见操作

该`IDatabase`接口包括其他几种使用 Redis 缓存的方法。 有一些方法可以使用哈希、列表、集和排序集。

下面是使用单个密钥的一些较常见的代码, 可以读取接口的[源代码](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs)以查看完整列表。

| 方法 | 说明 |
|--------|-------------|
| `CreateBatch` | 创建一_组_将作为单个单元发送到服务器但不一定作为一个单元进行处理的操作。 |
| `CreateTransaction` | 创建一组将作为单个单元发送到服务器_并_在服务器上作为一个单元进行处理的操作。 |
| `KeyDelete` | 删除键/值。 |
| `KeyExists` | 返回给定的键是否存在于缓存中。 |
| `KeyExpire` | 在项上设置生存时间 (TTL) 过期时间。 |
| `KeyRename` | 重命名密钥。 |
| `KeyTimeToLive` | 返回键的 TTL。 |
| `KeyType` | 返回存储在键上的值的类型的字符串表示形式。 可返回的不同类型为: string、list、set、zset 和 hash。 |
       
### <a name="executing-other-commands"></a>执行其他命令

`IDatabase`对象具有`Execute`和`ExecuteAsync`方法, 可用于将文本命令传递给 Redis 服务器。 例如：

```csharp
var result = db.Execute("ping");
Console.WriteLine(result.ToString()); // displays: "PONG"
```

和方法返回一个包含`RedisResult`以下两个属性的数据持有者的对象: `ExecuteAsync` `Execute`

- `Type`这将返回`string`指示结果的类型-"STRING"、"INTEGER" 等的类型。
- `IsNull`要在结果为`null`时检测到的 true/false 值。

然后, 可以在`ToString()`上使用`RedisResult`来获取实际返回值。

您可以使用`Execute`执行任何支持的命令-例如, 我们可以获取连接到缓存的所有客户端 ("客户端列表"):

```csharp
var result = await db.ExecuteAsync("client", "list");
Console.WriteLine($"Type = {result.Type}\r\nResult = {result}");
```

这将输出所有连接的客户端:

```output
Type = BulkString
Result = id=9469 addr=16.183.122.154:54961 fd=18 name=DESKTOP-AAAAAA age=0 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=subscribe numops=5
id=9470 addr=16.183.122.155:54967 fd=13 name=DESKTOP-BBBBBB age=0 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=client numops=17
```

### <a name="storing-more-complex-values"></a>存储更复杂的值
Redis 面向二进制安全字符串, 但您可以通过将它们序列化为文本格式 (通常为 XML 或 JSON) 来缓冲对象图。 例如, 对于我们的统计信息, 我们有一个`GameStats`如下所示的对象:

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

我们可以使用**newtonsoft.json**库将此对象的实例转换为字符串:

```csharp
var stat = new GameStat("Soccer", new DateTime(1950, 7, 16), "FIFA World Cup", 
                new[] { "Uruguay", "Brazil" },
                new[] { ("Uruguay", 2), ("Brazil", 1) });

string serializedValue = Newtonsoft.Json.JsonConvert.SerializeObject(stat);
bool added = db.StringSet("event:1950-world-cup", serializedValue);
```

我们可以检索它, 并使用反向进程将其转换回对象:

```csharp
var result = db.StringGet("event:1950-world-cup");
var stat = Newtonsoft.Json.JsonConvert.DeserializeObject<GameStat>(result.ToString());
Console.WriteLine(stat.Sport); // displays "Soccer"
```

## <a name="cleaning-up-the-connection"></a>清理连接
完成 Redis 连接后, 即可**释放** `ConnectionMultiplexer`。 这将关闭所有连接并关闭与服务器的通信。

```csharp
redisConnection.Dispose();
redisConnection = null;
```

让我们创建一个应用程序, 并使用我们的 Redis 缓存进行一些简单的操作。