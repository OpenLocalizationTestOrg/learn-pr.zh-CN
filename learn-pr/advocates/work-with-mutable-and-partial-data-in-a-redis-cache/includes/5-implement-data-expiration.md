<span data-ttu-id="e28c9-101">在这里, 你将向 Redis 的 Azure 缓存中的数据添加过期时间。</span><span class="sxs-lookup"><span data-stu-id="e28c9-101">Here, you'll add an expiration time to our data in the Azure Cache for Redis.</span></span>

## <a name="add-an-expiration-time"></a><span data-ttu-id="e28c9-102">添加过期时间</span><span class="sxs-lookup"><span data-stu-id="e28c9-102">Add an expiration time</span></span>

<span data-ttu-id="e28c9-103">在上一个练习中, 我们保留了**Program.cs**中的以下代码。</span><span class="sxs-lookup"><span data-stu-id="e28c9-103">In the last exercise, we left off with the following code in **Program.cs**.</span></span>

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

<span data-ttu-id="e28c9-104">让我们为**MyKey1**和**MyKey2**添加15秒的有效期。</span><span class="sxs-lookup"><span data-stu-id="e28c9-104">Let’s add an expiration of 15 seconds to both **MyKey1** and **MyKey2**.</span></span>

<span data-ttu-id="e28c9-105">在提交事务之前添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="e28c9-105">Add the following code before you commit the transaction:</span></span>

```csharp
//Add an expiration time
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey1", 15));
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey2", 15));
```

<span data-ttu-id="e28c9-106">在此代码中, "**过期**" 方法是**RedisNativeClient**的一部分。</span><span class="sxs-lookup"><span data-stu-id="e28c9-106">In this code, the **Expire** method is a part of the **RedisNativeClient**.</span></span> <span data-ttu-id="e28c9-107">若要访问此方法, 必须先转换对象。</span><span class="sxs-lookup"><span data-stu-id="e28c9-107">To access the method, we must first cast our object.</span></span>

## <a name="verify-the-expiration"></a><span data-ttu-id="e28c9-108">验证过期</span><span class="sxs-lookup"><span data-stu-id="e28c9-108">Verify the expiration</span></span>

<span data-ttu-id="e28c9-109">现在我们添加了代码来终止我们的数据, 让我们运行该程序并检查数据是否已从 Redis 的 Azure 缓存中删除。</span><span class="sxs-lookup"><span data-stu-id="e28c9-109">Now that we added the code to expire our data, let's run the program and check that the data is removed from Azure Cache for Redis.</span></span>

1. <span data-ttu-id="e28c9-110">运行该程序。</span><span class="sxs-lookup"><span data-stu-id="e28c9-110">Run the program.</span></span>

    ```bash
    dotnet run
    ```

1. <span data-ttu-id="e28c9-111">在 azure 门户中切换回 Redis 控制台的 azure 缓存。</span><span class="sxs-lookup"><span data-stu-id="e28c9-111">Switch back to the Azure Cache for Redis console in the Azure portal.</span></span>

1. <span data-ttu-id="e28c9-112">若要验证数据是否仍然存在, 请发出以下命令:</span><span class="sxs-lookup"><span data-stu-id="e28c9-112">To verify that the data is still there, issue the following command:</span></span>

    ```console
    get MyKey1
    ```

1. <span data-ttu-id="e28c9-113">15秒后, 再次发出此命令。</span><span class="sxs-lookup"><span data-stu-id="e28c9-113">After 15 seconds, issue the command again.</span></span> <span data-ttu-id="e28c9-114">您应该会看到数据已不再存在。</span><span class="sxs-lookup"><span data-stu-id="e28c9-114">You should see that the data is no longer there.</span></span>

    ![Redis 控制台的 Azure 缓存的屏幕截图, 显示 MyKey1 的值为零](../media/6-redis-console-data-expiration.png)