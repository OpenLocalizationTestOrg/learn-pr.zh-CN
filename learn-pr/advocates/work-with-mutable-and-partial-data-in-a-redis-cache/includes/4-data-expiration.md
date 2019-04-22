数据并非始终是永久性的, 有时您想要将其在特定时间删除。 例如, 在即时消息应用程序中, 用户可以设置组聊天的显示名称。 但是, 您希望名称在一小时后重置。 为此, 您可以编写自己的服务器端逻辑来设置小时计时器并删除名称。 但是, Redis 的 Azure 缓存支持数据过期, 这是一项功能, 可以自动执行此功能, 而无需编写额外的逻辑。

在这里, 你将了解用于实现数据过期的常见 Redis 命令。

## <a name="what-is-data-expiration"></a>什么是数据过期？

数据过期是一项功能, 可在设定的一段时间后自动删除缓存中的密钥和值。

## <a name="why-use-data-expiration"></a>为什么要使用数据过期？

数据过期通常在存储数据的生存期较短的情况下使用。  这一点很重要, 因为 Redis 的 Azure 缓存是内存中的数据库, 并且您没有足够的内存可供您使用, 如存储在磁盘上。 由于具有 Redis 的 Azure 缓存的存储空间有限, 因此您需要确保仅存储重要数据。 如果数据不需要很长一段时间, 请确保设置了过期时间。

## <a name="how-to-use-data-expiration-in-azure-cache-for-redis"></a>如何在 Redis 中使用 Azure 缓存中的数据过期

在 Redis 的 Azure 缓存中实施和管理数据过期的命令有不同之处:

- `EXPIRE`: 设置一个密钥的超时值 (以秒为单位)
- `PEXPIRE`: 设置密钥的超时值 (以毫秒为单位)
- `EXPIREAT`: 使用绝对 Unix 时间戳 (以秒为单位) 设置键的超时值
- `PEXPIREAT`: 使用绝对 Unix 时间戳 (以毫秒为单位) 设置密钥的超时值
- `TTL`: 返回密钥必须在几秒内生存的剩余时间
- `PTTL`: 返回键必须以毫秒为单位生存的剩余时间
- `PERSIST`: 使密钥永不过期

最常见的命令是`EXPIRE`, 我们将在整个模块中使用它。

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a>使用 c # 和 ServiceStack 的数据过期示例 Redis

请记住, 在使用客户端库 (如**ServiceStack**) 时, 我们不必担心为 Redis 命令记住低级别 Azure 缓存。 相反, 我们可以使用简单的 c # 方法。

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

Redis 的 Azure 缓存允许您在经过一段时间后使用数据过期来自动删除数据。 这一点很重要, 因为 Redis 的 Azure 缓存是内存中的数据库, 并且您没有像将数据存储在磁盘上那样多的可用内存。 如果要存储的数据不需要很长时间, 请确保设置了一个过期时间。