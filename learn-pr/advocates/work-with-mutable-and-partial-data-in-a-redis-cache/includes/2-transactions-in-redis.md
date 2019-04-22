<span data-ttu-id="89f14-101">有时, 您必须确保同时执行多个操作。</span><span class="sxs-lookup"><span data-stu-id="89f14-101">There are times when you must guarantee that multiple operations execute together.</span></span> <span data-ttu-id="89f14-102">例如, 在即时消息应用程序中, 用户可以将单个图片、单个短信或图片和文本消息一起发送。</span><span class="sxs-lookup"><span data-stu-id="89f14-102">For example, in your instant messaging application, users can send an individual picture, an individual text message, or a picture and text message together.</span></span> <span data-ttu-id="89f14-103">当用户选择同时发送图片和文本消息时, 必须确保组的其他成员同时收到它们。</span><span class="sxs-lookup"><span data-stu-id="89f14-103">When the user chooses to send a picture and text message together, you must ensure that other members of the group receive them at the same time.</span></span> <span data-ttu-id="89f14-104">这一点很重要, 因为如果不一起接收图片和短信, 则可能会在图片和短信之间发送单独的邮件。</span><span class="sxs-lookup"><span data-stu-id="89f14-104">This is important because if a picture and text message are not received together, it’s possible that a separate message could be sent in between the picture and text message.</span></span> <span data-ttu-id="89f14-105">这可能会使整体对话变得混乱。</span><span class="sxs-lookup"><span data-stu-id="89f14-105">That could make the overall conversation confusing.</span></span>

<span data-ttu-id="89f14-106">在这里, 我们将介绍如何在 Azure 缓存中为 Redis 创建事务, 以确保同时执行多个操作。</span><span class="sxs-lookup"><span data-stu-id="89f14-106">Here, we'll look at how to create a transaction in Azure Cache for Redis to guarantee that multiple operations are executed together.</span></span>

## <a name="creating-and-running-transactions"></a><span data-ttu-id="89f14-107">创建和运行事务</span><span class="sxs-lookup"><span data-stu-id="89f14-107">Creating and running transactions</span></span>

<span data-ttu-id="89f14-108">Redis 中的事务通过将多个要作为组执行的命令排列在一起。</span><span class="sxs-lookup"><span data-stu-id="89f14-108">Transactions in Redis work by queueing multiple commands to be executed as a group.</span></span> <span data-ttu-id="89f14-109">执行事务时, 可以保证在不出现任何其他命令的情况下执行在其内部排队的命令。</span><span class="sxs-lookup"><span data-stu-id="89f14-109">When a transaction is executed, the commands queued inside of it are guaranteed to execute without any other commands from other clients interleaved between them.</span></span>

<span data-ttu-id="89f14-110">若要开始事务块, 请输入`MULTI`命令。</span><span class="sxs-lookup"><span data-stu-id="89f14-110">To begin a transaction block, enter the `MULTI` command.</span></span> <span data-ttu-id="89f14-111">其他命令将被排队, 且不会立即执行。</span><span class="sxs-lookup"><span data-stu-id="89f14-111">Further commands will be queued and not executed immediately.</span></span> <span data-ttu-id="89f14-112">运行`EXEC`命令将以事务性单位执行所有排队命令。</span><span class="sxs-lookup"><span data-stu-id="89f14-112">Running the `EXEC` command will execute all of the queued commands as a transactional unit.</span></span> <span data-ttu-id="89f14-113">如果您决定在对命令进行排队时中止打开的事务, 则运行`DISCARD`该命令将关闭事务块, 而不运行_任何_已排队的命令。</span><span class="sxs-lookup"><span data-stu-id="89f14-113">If you decide you want to abort an open transaction while queuing commands, running the `DISCARD` command will close the transaction block without running _any_ of the queued commands.</span></span>

<span data-ttu-id="89f14-114">Redis 事务不支持回滚的概念。</span><span class="sxs-lookup"><span data-stu-id="89f14-114">Redis transactions do not support the concept of rollback.</span></span> <span data-ttu-id="89f14-115">如果将包含错误语法的命令排队到事务块中, 该块将保持打开状态, 但如果您尝试使用`EXEC`执行它, 则会自动丢弃该块。</span><span class="sxs-lookup"><span data-stu-id="89f14-115">If you queue a command with incorrect syntax into a transaction block, the block will remain open, but will automatically be discarded if you attempt to execute it with `EXEC`.</span></span> <span data-ttu-id="89f14-116">在执行_过程中_失败的事务中的命令`EXEC` (如果调用之后) 不会导致事务中止或回滚&mdash; Redis 仍将运行所有命令并认为事务已成功完成。</span><span class="sxs-lookup"><span data-stu-id="89f14-116">Commands in a transaction that fail _during_ execution (after `EXEC` is called) do not cause a transaction to be aborted or rolled back &mdash; Redis will still run all of the commands and consider the transaction to have completed successfully.</span></span>

## <a name="redis-transactions-with-servicestackredis"></a><span data-ttu-id="89f14-117">Redis 事务与 ServiceStack。 Redis</span><span class="sxs-lookup"><span data-stu-id="89f14-117">Redis transactions with ServiceStack.Redis</span></span>

<span data-ttu-id="89f14-118">**ServiceStack**是一个 c # 客户端库, 用于与 Redis 的 Azure 缓存进行交互。</span><span class="sxs-lookup"><span data-stu-id="89f14-118">**ServiceStack.Redis** is a C# client library for interacting with Azure Cache for Redis.</span></span>

<span data-ttu-id="89f14-119">Redis 中的事务是通过调用`IRedisClient.CreateTransaction()`创建的。</span><span class="sxs-lookup"><span data-stu-id="89f14-119">Transactions in ServiceStack.Redis are created by calling `IRedisClient.CreateTransaction()`.</span></span> <span data-ttu-id="89f14-120">返回`IRedisTransaction`的对象可以有多个命令在其中排队`QueueCommand()`。</span><span class="sxs-lookup"><span data-stu-id="89f14-120">The `IRedisTransaction` object that is returned can have multiple commands queued into it with `QueueCommand()`.</span></span> <span data-ttu-id="89f14-121">对`Commit()`事务对象的调用将执行该对象。</span><span class="sxs-lookup"><span data-stu-id="89f14-121">Calling `Commit()` on the transaction object will execute it.</span></span>

<span data-ttu-id="89f14-122">`IRedisTransaction`对象是可释放的, 并将自动`DISCARD`发出命令, 如果在`Commit()`调用之前已释放。</span><span class="sxs-lookup"><span data-stu-id="89f14-122">`IRedisTransaction` objects are disposable, and will automatically issue a `DISCARD` command if disposed before calling `Commit()`.</span></span> <span data-ttu-id="89f14-123">此功能适用于 c # 的`using`块: 如果由于任何原因不提交事务, 可以信任事务将自动丢弃, 以便可以继续使用 Redis 连接。</span><span class="sxs-lookup"><span data-stu-id="89f14-123">This feature works well with C#'s `using` blocks: if you don't commit a transaction for any reason, you can trust that the transaction will automatically be discarded so that the Redis connection can continue to be used.</span></span>

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a><span data-ttu-id="89f14-124">使用 c # 和 Redis 客户端创建事务 ServiceStack</span><span class="sxs-lookup"><span data-stu-id="89f14-124">Create a transaction using C# and the ServiceStack.Redis client</span></span>

<span data-ttu-id="89f14-125">下面的示例展示了如何使用 ServiceStack 创建可发送包含图片 URL 和短信内容的邮件的事务。</span><span class="sxs-lookup"><span data-stu-id="89f14-125">Here's an example of using ServiceStack.Redis to create a transaction that can send a message that includes a picture URL and the contents of a text message.</span></span>

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

<span data-ttu-id="89f14-126">事务可确保同时执行多个操作, 而不会在它们之间执行其他客户端的操作。</span><span class="sxs-lookup"><span data-stu-id="89f14-126">Transactions ensure that multiple operations are executed together without operations from other clients in between them.</span></span> <span data-ttu-id="89f14-127">使用`MULTI`命令创建事务。</span><span class="sxs-lookup"><span data-stu-id="89f14-127">You create a transaction using the `MULTI` command.</span></span> <span data-ttu-id="89f14-128">使用 ServiceStack, 可以使用`CreateTransaction()`方法。</span><span class="sxs-lookup"><span data-stu-id="89f14-128">With ServiceStack.Redis, you use the `CreateTransaction()` method.</span></span>