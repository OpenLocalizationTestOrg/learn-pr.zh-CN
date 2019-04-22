有时, 您必须确保同时执行多个操作。 例如, 在即时消息应用程序中, 用户可以将单个图片、单个短信或图片和文本消息一起发送。 当用户选择同时发送图片和文本消息时, 必须确保组的其他成员同时收到它们。 这一点很重要, 因为如果不一起接收图片和短信, 则可能会在图片和短信之间发送单独的邮件。 这可能会使整体对话变得混乱。

在这里, 我们将介绍如何在 Azure 缓存中为 Redis 创建事务, 以确保同时执行多个操作。

## <a name="creating-and-running-transactions"></a>创建和运行事务

Redis 中的事务通过将多个要作为组执行的命令排列在一起。 执行事务时, 可以保证在不出现任何其他命令的情况下执行在其内部排队的命令。

若要开始事务块, 请输入`MULTI`命令。 其他命令将被排队, 且不会立即执行。 运行`EXEC`命令将以事务性单位执行所有排队命令。 如果您决定在对命令进行排队时中止打开的事务, 则运行`DISCARD`该命令将关闭事务块, 而不运行_任何_已排队的命令。

Redis 事务不支持回滚的概念。 如果将包含错误语法的命令排队到事务块中, 该块将保持打开状态, 但如果您尝试使用`EXEC`执行它, 则会自动丢弃该块。 在执行_过程中_失败的事务中的命令`EXEC` (如果调用之后) 不会导致事务中止或回滚&mdash; Redis 仍将运行所有命令并认为事务已成功完成。

## <a name="redis-transactions-with-servicestackredis"></a>Redis 事务与 ServiceStack。 Redis

**ServiceStack**是一个 c # 客户端库, 用于与 Redis 的 Azure 缓存进行交互。

Redis 中的事务是通过调用`IRedisClient.CreateTransaction()`创建的。 返回`IRedisTransaction`的对象可以有多个命令在其中排队`QueueCommand()`。 对`Commit()`事务对象的调用将执行该对象。

`IRedisTransaction`对象是可释放的, 并将自动`DISCARD`发出命令, 如果在`Commit()`调用之前已释放。 此功能适用于 c # 的`using`块: 如果由于任何原因不提交事务, 可以信任事务将自动丢弃, 以便可以继续使用 Redis 连接。

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a>使用 c # 和 Redis 客户端创建事务 ServiceStack

下面的示例展示了如何使用 ServiceStack 创建可发送包含图片 URL 和短信内容的邮件的事务。

```csharp
public bool SendPictureAndText(string groupChatID, string text, string pictureURL)
{
    bool transactionResult = false;

    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    using (var transaction = redisClient.CreateTransaction())
    {
        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, pictureURL));
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, text));

        //Commit and get result of transaction
        transactionResult = transaction.Commit();
    }

    return transactionResult;
}
```

事务可确保同时执行多个操作, 而不会在它们之间执行其他客户端的操作。 使用`MULTI`命令创建事务。 使用 ServiceStack, 可以使用`CreateTransaction()`方法。