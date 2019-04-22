<span data-ttu-id="1452b-101">现在, 我们想要通过编写代码来读取队列中的下一封邮件, 并对其进行处理并将其从队列中删除来完成该应用程序。</span><span class="sxs-lookup"><span data-stu-id="1452b-101">Now we want to complete the application by writing code to read the next message in the queue, process it, and delete it from the queue.</span></span> 

<span data-ttu-id="1452b-102">我们打算将此代码放入同一个应用程序中, 并在未传递任何参数时执行此代码, 但在我们的新闻服务方案中, 我们实际上会将此代码放入中间层服务器来处理这些情景。</span><span class="sxs-lookup"><span data-stu-id="1452b-102">We're going to place this code into the same application and execute it when you don't pass any parameters, however in our news service scenario, we would really place this code into our middle-tier servers to process the stories.</span></span>

## <a name="dequeue-a-message"></a><span data-ttu-id="1452b-103">取消邮件排队</span><span class="sxs-lookup"><span data-stu-id="1452b-103">Dequeue a message</span></span>

<span data-ttu-id="1452b-104">让我们添加一个新方法, 从队列中检索下一封邮件。</span><span class="sxs-lookup"><span data-stu-id="1452b-104">Let's add a new method that retrieves the next message from the queue.</span></span>

1. <span data-ttu-id="1452b-105">在编辑器`Program.cs`中打开源文件。</span><span class="sxs-lookup"><span data-stu-id="1452b-105">Open the `Program.cs` source file in your editor.</span></span>

1. <span data-ttu-id="1452b-106">在名为`Program` `ReceiveArticleAsync`的类中创建静态方法, 该方法不采用任何`Task<string>`参数并返回。</span><span class="sxs-lookup"><span data-stu-id="1452b-106">Create a static method in the `Program` class named `ReceiveArticleAsync` that takes no parameters and returns a `Task<string>`.</span></span> <span data-ttu-id="1452b-107">我们将使用此方法从队列中提取新闻文章并将其返回。</span><span class="sxs-lookup"><span data-stu-id="1452b-107">We'll use this method to pull a news article from the queue and return it.</span></span>
    - <span data-ttu-id="1452b-108">继续执行并将`async`关键字添加到方法, 因为我们将使用一些基于异步`Task`的方法。</span><span class="sxs-lookup"><span data-stu-id="1452b-108">Go ahead and add the `async` keyword to the method since we'll be using some asynchronous `Task`-based methods.</span></span>

    ```csharp
    static async Task<string> ReceiveArticleAsync()
    {
    }

1. All of the setup code to get a `CloudQueue` will be identical to what we did in the last exercise. Code duplication is a bad habit, even in samples so go ahead and, refactor the code that obtains the `CloudQueue` to a new method named `GetQueue` and change the `SendArticleAsync` to use your new method.
     - Make sure to leave the code that _creates_ the queue in the `SendArticleAsync` method; remember only the **publisher** should create the queue.

    ```csharp
    const string ConnectionString = ...;
    // ...

    static CloudQueue GetQueue()
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        return queueClient.GetQueueReference("newsqueue");
    }
    ```
    
1. <span data-ttu-id="1452b-109">在您`ReceiveArticleAsync`的方法中, 调用`GetQueue`新方法以检索您的队列引用并将其分配给变量。</span><span class="sxs-lookup"><span data-stu-id="1452b-109">In your `ReceiveArticleAsync` method, call the new `GetQueue` method to retrieve your queue reference and assign it to a variable.</span></span>

1. <span data-ttu-id="1452b-110">接下来, 对`ExistsAsync` `CloudQueue`对象调用方法;这将返回是否已创建队列。</span><span class="sxs-lookup"><span data-stu-id="1452b-110">Next, call the `ExistsAsync` method on the `CloudQueue` object; this will return whether the queue has been created.</span></span> <span data-ttu-id="1452b-111">如果我们尝试从不存在的队列中检索邮件, 该 API 将引发异常。</span><span class="sxs-lookup"><span data-stu-id="1452b-111">If we attempt to retrieve a message from a non-existent queue, the API will throw an exception.</span></span>
    - <span data-ttu-id="1452b-112">此方法是异步方法, `await`因此可用于获取返回值。</span><span class="sxs-lookup"><span data-stu-id="1452b-112">This method is asynchronous so use `await` to get the return value.</span></span>
    - <span data-ttu-id="1452b-113">您应该已经对`async` `ReceiveArticleAsync`方法使用了关键字, 但现在不添加它。</span><span class="sxs-lookup"><span data-stu-id="1452b-113">You should already have the `async` keyword on the `ReceiveArticleAsync` method, but if not add it now.</span></span>


1. <span data-ttu-id="1452b-114">将使用`if`返回值的块添加到`ExistsAsync`。</span><span class="sxs-lookup"><span data-stu-id="1452b-114">Add an `if` block that uses the return value from `ExistsAsync`.</span></span> <span data-ttu-id="1452b-115">我们将添加代码以将队列中的值读取到块中。</span><span class="sxs-lookup"><span data-stu-id="1452b-115">We'll add our code to read a value from the queue into the block.</span></span> <span data-ttu-id="1452b-116">向方法添加最后一个返回字符串, 以指示未读取任何值。</span><span class="sxs-lookup"><span data-stu-id="1452b-116">Add a final return string to the method that indicates no value was read.</span></span> <span data-ttu-id="1452b-117">您的方法应如下所示:</span><span class="sxs-lookup"><span data-stu-id="1452b-117">Your method should be looking something like this:</span></span>

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
    }

    return "<queue empty or not created>";
}
```

1. <span data-ttu-id="1452b-118">对`GetMessageAsync`要从`CloudQueue`队列中获取第一个`CloudQueueMessage`的对象的调用。</span><span class="sxs-lookup"><span data-stu-id="1452b-118">Call `GetMessageAsync` on the `CloudQueue` object to get the first `CloudQueueMessage` from the queue.</span></span> <span data-ttu-id="1452b-119">如果队列是空的`null` , 返回值将为。</span><span class="sxs-lookup"><span data-stu-id="1452b-119">The return value will be `null` if the queue is empty.</span></span>

1. <span data-ttu-id="1452b-120">如果不为 null, 则对该`AsString` `CloudQueueMessage`对象使用属性以获取邮件的内容。</span><span class="sxs-lookup"><span data-stu-id="1452b-120">If it's non-null, use the `AsString` property on the `CloudQueueMessage` object to get the contents of the message.</span></span>

1. <span data-ttu-id="1452b-121">对`DeleteMessageAsync`要从`CloudQueue`队列中删除邮件的对象调用。</span><span class="sxs-lookup"><span data-stu-id="1452b-121">Call `DeleteMessageAsync` on the `CloudQueue` object to delete the message from the queue.</span></span>

<span data-ttu-id="1452b-122">最终方法实现应类似于:</span><span class="sxs-lookup"><span data-stu-id="1452b-122">The final method implementation should resemble:</span></span>

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
        CloudQueueMessage retrievedArticle = await queue.GetMessageAsync();
        if (retrievedArticle != null)
        {
            string newsMessage = retrievedArticle.AsString;
            await queue.DeleteMessageAsync(retrievedArticle);
            return newsMessage;
        }
    }

    return "<queue empty or not created>";
}
```

## <a name="call-the-receivearticleasync-method"></a><span data-ttu-id="1452b-123">调用 ReceiveArticleAsync 方法</span><span class="sxs-lookup"><span data-stu-id="1452b-123">Call the ReceiveArticleAsync method</span></span>

<span data-ttu-id="1452b-124">最后, 让我们添加支持, 以调用我们的新方法。</span><span class="sxs-lookup"><span data-stu-id="1452b-124">Finally, let's add support to invoke our new method.</span></span> <span data-ttu-id="1452b-125">当我们未将任何参数传递到程序中时, 我们将执行此操作。</span><span class="sxs-lookup"><span data-stu-id="1452b-125">We'll do this when we don't pass any parameters into the program.</span></span>

1. <span data-ttu-id="1452b-126">找到您`Main`之前添加的用于`if`查找参数的方法并专门添加的块。</span><span class="sxs-lookup"><span data-stu-id="1452b-126">Locate the `Main` method and specifically the `if` block you added earlier to look for parameters.</span></span>

1. <span data-ttu-id="1452b-127">添加一个`else`条件并调用`ReceiveArticleAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="1452b-127">Add an `else` condition and call the `ReceiveArticleAsync` method.</span></span> 

1. <span data-ttu-id="1452b-128">由于它是异步的, 因此`await`请使用关键字检索结果并将其打印到控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="1452b-128">Since it's asynchronous, use the `await` keyword to retrieve the result and print it to the console window.</span></span> <span data-ttu-id="1452b-129">如果未将应用转换为 c # 7.1, 则可以使用返回的任务中`Result`的属性获取该值。</span><span class="sxs-lookup"><span data-stu-id="1452b-129">If you didn't convert your app to C# 7.1, you can get the value using the `Result` property from the returning task.</span></span>

<span data-ttu-id="1452b-130">您的代码应类似于以下内容:</span><span class="sxs-lookup"><span data-stu-id="1452b-130">Your code should look something like:</span></span>

```csharp
if (args.Length > 0)
{
    // ...
}
else
{
    string value = await ReceiveArticleAsync();
    Console.WriteLine($"Received {value}");
}
```

## <a name="execute-the-application"></a><span data-ttu-id="1452b-131">执行应用程序</span><span class="sxs-lookup"><span data-stu-id="1452b-131">Execute the application</span></span>

<span data-ttu-id="1452b-132">代码现已完成。</span><span class="sxs-lookup"><span data-stu-id="1452b-132">The code is now complete.</span></span> <span data-ttu-id="1452b-133">它现在可以发送和检索邮件。</span><span class="sxs-lookup"><span data-stu-id="1452b-133">It can now send and retrieve messages.</span></span> 

> [!WARNING]
> <span data-ttu-id="1452b-134">在生成和运行程序之前, 请确保已将所有文件保存在联机编辑器中。</span><span class="sxs-lookup"><span data-stu-id="1452b-134">Make sure you have saved all the files in the online editor before you build and run the program.</span></span>

<span data-ttu-id="1452b-135">若要对其进行`dotnet run`测试, 请使用并传递参数以发送邮件, 并保留用于读取单个邮件的参数。</span><span class="sxs-lookup"><span data-stu-id="1452b-135">To test it, use `dotnet run` and pass parameters to send messages, and leave off parameters to read a single message.</span></span>

<span data-ttu-id="1452b-136">如果要测试队列不存在的时间, 可以使用 Azure CLI 删除队列 (和所有数据)。</span><span class="sxs-lookup"><span data-stu-id="1452b-136">If you want to test when a queue doesn't exist, you can delete the queue (and all the data) with the Azure CLI.</span></span> <span data-ttu-id="1452b-137">请确保替换`<connection-string>`参数 (或设置环境变量)。</span><span class="sxs-lookup"><span data-stu-id="1452b-137">Make sure to replace the `<connection-string>` parameter (or set the environment variable).</span></span>

```azurecli
az storage queue delete --name newsqueue --connection-string <connection-string> 
```

<span data-ttu-id="1452b-138">下次添加邮件时, 应重新创建该队列。</span><span class="sxs-lookup"><span data-stu-id="1452b-138">The next time you add a message, the queue should be re-created.</span></span>

> [!NOTE]
> <span data-ttu-id="1452b-139">删除操作实际上是异步进行的。</span><span class="sxs-lookup"><span data-stu-id="1452b-139">The delete operation actually occurs asynchronously.</span></span> <span data-ttu-id="1452b-140">如果尚未完成, 则在尝试重新创建队列时可能会收到异常。</span><span class="sxs-lookup"><span data-stu-id="1452b-140">If it has not completed you may get an exception when you attempt to re-create the queue.</span></span>