在这里, 你将向 Redis 的 Azure 缓存中的数据添加过期时间。

## <a name="add-an-expiration-time"></a>添加过期时间

在上一个练习中, 我们保留了**Program.cs**中的以下代码。

```csharp
bool transactionResult = false;

using (RedisClient redisClient = new RedisClient(redisConnectionString))
using (var transaction = redisClient.CreateTransaction())
{
    //Add multiple operations to the transaction
    transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
    transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

    //Commit and get result of transaction
    transactionResult = transaction.Commit();
}

if(transactionResult)
{
    Console.WriteLine("Transaction committed");
}
else
{
    Console.WriteLine("Transaction failed to commit");
}
```

让我们为**MyKey1**和**MyKey2**添加15秒的有效期。

在提交事务之前添加以下代码:

```csharp
//Add an expiration time
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey1", 15));
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey2", 15));
```

在此代码中, "**过期**" 方法是**RedisNativeClient**的一部分。 若要访问此方法, 必须先转换对象。

## <a name="verify-the-expiration"></a>验证过期

现在我们添加了代码来终止我们的数据, 让我们运行该程序并检查数据是否已从 Redis 的 Azure 缓存中删除。

1. 运行该程序。

    ```bash
    dotnet run
    ```

1. 在 azure 门户中切换回 Redis 控制台的 azure 缓存。

1. 若要验证数据是否仍然存在, 请发出以下命令:

    ```console
    get MyKey1
    ```

1. 15秒后, 再次发出此命令。 您应该会看到数据已不再存在。

    ![Redis 控制台的 Azure 缓存的屏幕截图, 显示 MyKey1 的值为零](../media/6-redis-console-data-expiration.png)