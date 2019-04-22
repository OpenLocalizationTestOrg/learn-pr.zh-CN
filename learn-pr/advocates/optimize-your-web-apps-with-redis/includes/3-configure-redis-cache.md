您的体育统计信息开发团队已决定缓存可显著提高最近请求的数据的性能。 下一步是为 Redis 实例创建和配置 Azure 缓存。

## <a name="create-and-configure-the-azure-cache-for-redis-instance"></a>创建和配置 Redis 实例的 Azure 缓存

您可以使用 azure 门户、azure CLI 或 azure PowerShell 创建 Redis 缓存。 您需要确定几个参数, 以便正确配置缓存以满足您的需求。

### <a name="name"></a>名称

Redis 缓存将需要一个全局唯一名称。 名称在 Azure 中必须是唯一的, 因为它用于生成面向公众的 URL 以连接服务并与之通信。

名称必须介于1到63个字符之间, 由数字、字母和 '-' 字符组成。 缓存名称不能以 "-" 字符开头或结尾, 且连续的 "-" 字符无效。

### <a name="resource-group"></a>资源组

Redis 的 Azure 缓存是一个托管资源, 需要_资源组_所有者。 您可以创建新的资源组, 也可以在您所属的订阅中使用现有资源组。

### <a name="location"></a>位置

您将需要通过选择 Azure 区域来决定 Redis 缓存的物理位置。 应始终将缓存实例和应用程序放在同一区域中。 连接到不同区域中的缓存会显著增加延迟并降低可靠性。 如果要连接到 Azure 外部的缓存, 请选择要在使用数据的应用程序运行的位置附近的位置。

> [!IMPORTANT]
> 尽可能将 Redis 缓存放在数据_使用者_附近。

### <a name="pricing-tier"></a>定价层

如最后一个设备中所述, 有三个可用于 Redis 的 Azure 缓存定价层。

- **基本**: 适用于开发/测试的基本缓存。 限制为单个服务器、53 GB 的内存和20000连接。 此服务层没有 SLA。
- **标准**: 支持复制的生产缓存, 并包含 99.99% SLA。 它支持两台服务器 (主/从), 并具有与基本层相同的内存/连接限制。
- **Premium**: 在标准层上构建的企业级, 包括暂留、聚集和扩展缓存支持。 这是具有高达 530 GB 内存和40000同时连接的高性能层。

您可以控制每个层上可用的缓存内存量-这是通过从 C0-C6 为 Basic/Standard 和 P0-P4 为 Premium 选择缓存级别选择的。 有关详细信息, 请查看 "[定价" 页面](https://azure.microsoft.com/pricing/details/cache/)。

> [!TIP]
> Microsoft 建议您始终对生产系统使用标准或高级层。 基本层是单个节点系统, 无数据复制和无 SLA。 此外, 至少使用 C1 缓存。 C0 缓存实际上适用于简单的开发/测试方案, 因为它们具有共享的 CPU 内核和非常少的内存。

高级层允许您以两种方式保留数据, 以提供灾难恢复:

1. RDB 持久化采用定期快照, 并且可以在出现故障时使用快照重建缓存。

    ![在新的 Redis 缓存实例上显示 RDB 持久性选项的 Azure 门户屏幕截图。](../media/3-redis-persistence-1.png)

2. AOF 持久性将每个写入操作保存到每秒至少保存一次的日志。 这将创建比 RDB 更大的文件, 但数据丢失较少。

    ![显示新 Redis 缓存实例上的 AOF 持久性选项的 Azure 门户屏幕截图。](../media/3-redis-persistence-2.png)

有几个其他设置仅适用于**高级**层。

### <a name="virtual-network-support"></a>虚拟网络支持

如果创建高级层 Redis 缓存, 则可以将其部署到云中的虚拟网络。 您的缓存将仅对同一虚拟网络中的其他虚拟机和应用程序可用。 当您的服务和缓存托管在 azure 中, 或通过 azure 虚拟网络 VPN 连接时, 这将提供更高级别的安全性。

### <a name="clustering-support"></a>群集支持

使用高级层 Redis 缓存, 可以实现群集以在多个节点之间自动拆分数据集。 若要实施群集, 请指定最大值为10的 shards 数。 产生的成本是原始节点的成本, 乘以 shards 的数量。

## <a name="accessing-the-redis-instance"></a>访问 Redis 实例

Redis 支持一组[已知命令](https://redis.io/commands)。 通常将命令作为`COMMAND parameter1 parameter2 parameter3`发出。

以下是您可以使用的一些常见命令:

| 指挥 | 说明 |
|---------|-------------|
| `ping` | Ping 服务器。 返回 "乒乓球"。 |
| `set [key] [value]` | 在缓存中设置键/值。 成功后返回 "确定"。 |
| `get [key]` | 从缓存中获取值。 |
| `exists [key]` | 如果**项**在缓存中存在, 则返回 "1", 如果不存在, 则返回 "0"。 |
| `type [key]` | 返回与给定**键**的值关联的类型。 |
| `incr [key]` | 将与**键**关联的给定值递增 "1"。 值必须为整数或双精度值。 这将返回新值。 |
| `incrby [key] [amount]` | 将与**键**关联的给定值递增指定的量。 值必须为整数或双精度值。 这将返回新值。 |
| `del [key]` | 删除与**键**关联的值。 |
| `flushdb` | 删除数据库中的_所有_键和值。 |

Redis 有一个命令行工具 (**Redis-cli**), 您可以使用它直接试用这些命令。 下面是一些示例。

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

下面的示例展示了如何使用`INCR`命令。 这是很方便的, 因为它们在使用缓存的_多个应用程序之间_提供了原子增量。

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

### <a name="adding-an-expiration-time-to-values"></a>将过期时间添加到值

缓存非常重要, 因为它允许我们将常用值存储在内存中。 但是, 我们还需要一种在值过时时过期值的方法。 在 Redis 中, 通过将_时间生存时间_(TTL) 应用到某个键来实现此目的。

当 TTL 过期时, 将自动删除密钥, 就像发出 DEL 命令一样。 下面是有关 TTL 到期的一些注意事项。

- 可以使用秒或毫秒精度设置过期时间。
- 过期时间解析始终为1毫秒。
- 有关过期的信息会复制并保存在磁盘上, 当 Redis 服务器保持停止时, 几乎会通过此时间传递 (这意味着 Redis 将保存密钥过期的日期)。

下面是一个过期的示例:

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

## <a name="accessing-a-redis-cache-from-a-client"></a>从客户端访问 Redis 缓存

若要连接到 Redis 实例的 Azure 缓存, 需要多条信息。 客户端需要缓存的主机名、端口和访问密钥。 您可以通过 "**设置 > 访问密钥**" 页面在 Azure 门户中检索此信息。 

- 主机名是缓存的公共 Internet 地址, 它是使用缓存名称创建的。 例如`sportsresults.redis.cache.windows.net`。

- 访问键充当缓存的密码。 创建了两个键: 主和辅助。 您可以使用两个键中的任意一个, 以在需要更改主键的情况下提供。 您可以将所有客户端切换到辅助密钥, 然后重新生成主键。 这将阻止使用原始主关键字的任何应用程序。 Microsoft 建议定期重新生成密钥, 就像你的个人密码一样。

> [!WARNING]
> 你的访问密钥应被视为机密信息, 请像对待密码那样对待。 拥有访问密钥的任何人都可以在缓存上执行任何操作!
