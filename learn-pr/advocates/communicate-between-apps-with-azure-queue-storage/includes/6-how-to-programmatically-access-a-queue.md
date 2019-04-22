<span data-ttu-id="db113-101">队列保留邮件-其形状已知的发件人应用程序和收件人应用程序的数据数据包。</span><span class="sxs-lookup"><span data-stu-id="db113-101">Queues hold messages - packets of data whose shape is known to the sender application and receiver application.</span></span> <span data-ttu-id="db113-102">发件人创建队列并添加邮件。</span><span class="sxs-lookup"><span data-stu-id="db113-102">The sender creates the queue and adds a message.</span></span> <span data-ttu-id="db113-103">收件人检索邮件, 对其进行处理, 然后从队列中删除邮件。</span><span class="sxs-lookup"><span data-stu-id="db113-103">The receiver retrieves a message, processes it, and then deletes the message from the queue.</span></span> <span data-ttu-id="db113-104">下图显示了此过程的典型流程。</span><span class="sxs-lookup"><span data-stu-id="db113-104">The following illustration shows a typical flow of this process.</span></span>

![显示通过 Azure 队列的典型邮件流的插图。](../media/6-message-flow.png)

<span data-ttu-id="db113-106">请注意`get` , `delete`和是单独的操作。</span><span class="sxs-lookup"><span data-stu-id="db113-106">Notice that `get` and `delete` are separate operations.</span></span> <span data-ttu-id="db113-107">这种排列处理接收器中的潜在故障并实现一种_至少称为一次性传递_的概念。</span><span class="sxs-lookup"><span data-stu-id="db113-107">This arrangement handles potential failures in the receiver and implements a concept called _at-least-once delivery_.</span></span> <span data-ttu-id="db113-108">接收器收到一条消息后, 该消息将保留在队列中, 但不可见30秒。</span><span class="sxs-lookup"><span data-stu-id="db113-108">After the receiver gets a message, that message remains in the queue but is invisible for 30 seconds.</span></span> <span data-ttu-id="db113-109">如果接收器在处理过程中崩溃或遇到断电故障, 则永远不会从队列中删除该邮件。</span><span class="sxs-lookup"><span data-stu-id="db113-109">If the receiver crashes or experiences a power failure during processing, then it will never delete the message from the queue.</span></span> <span data-ttu-id="db113-110">30秒后, 该邮件将重新显示在队列中, 并且收件人的另一个实例可以将其处理为完成。</span><span class="sxs-lookup"><span data-stu-id="db113-110">After 30 seconds, the message will reappear in the queue and another instance of the receiver can process it to completion.</span></span>

## <a name="the-azure-storage-client-library-for-net"></a><span data-ttu-id="db113-111">适用于 .net 的 Azure 存储客户端库</span><span class="sxs-lookup"><span data-stu-id="db113-111">The Azure Storage Client Library for .NET</span></span>

<span data-ttu-id="db113-112">**适用于 .net 的 Azure 存储客户端库**提供了用于表示您需要与之交互的每个对象的类型:</span><span class="sxs-lookup"><span data-stu-id="db113-112">The **Azure Storage Client Library for .NET** provides types to represent each of the objects you need to interact with:</span></span>

- <span data-ttu-id="db113-113">`CloudStorageAccount`表示你的 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="db113-113">`CloudStorageAccount` represents your Azure storage account.</span></span>
- <span data-ttu-id="db113-114">`CloudQueueClient`表示 Azure 队列存储。</span><span class="sxs-lookup"><span data-stu-id="db113-114">`CloudQueueClient` represents Azure Queue storage.</span></span>
- <span data-ttu-id="db113-115">`CloudQueue`表示您的队列实例之一。</span><span class="sxs-lookup"><span data-stu-id="db113-115">`CloudQueue` represents one of your queue instances.</span></span>
- <span data-ttu-id="db113-116">`CloudQueueMessage`代表一封邮件。</span><span class="sxs-lookup"><span data-stu-id="db113-116">`CloudQueueMessage` represents a message.</span></span>

<span data-ttu-id="db113-117">您将使用这些类来获取对您的队列的编程访问权限。</span><span class="sxs-lookup"><span data-stu-id="db113-117">You will use these classes to get programmatic access to your queue.</span></span> <span data-ttu-id="db113-118">库既有同步方法, 也有异步方法;您应首选使用异步版本以避免阻止客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="db113-118">The library has both synchronous and asynchronous methods; you should prefer to use the asynchronous versions to avoid blocking the client app.</span></span>

> [!NOTE]
> <span data-ttu-id="db113-119">**WindowsAzure** NuGet 包中提供了适用于 .net 的 Azure 存储客户端库。</span><span class="sxs-lookup"><span data-stu-id="db113-119">The Azure Storage Client Library for .NET is available in the **WindowsAzure.Storage** NuGet package.</span></span> <span data-ttu-id="db113-120">您可以通过 IDE、Azure CLI 或通过 PowerShell `Install-Package WindowsAzure.Storage`安装它。</span><span class="sxs-lookup"><span data-stu-id="db113-120">You can install it through an IDE, Azure CLI, or through PowerShell `Install-Package WindowsAzure.Storage`.</span></span>

## <a name="how-to-connect-to-a-queue"></a><span data-ttu-id="db113-121">如何连接到队列</span><span class="sxs-lookup"><span data-stu-id="db113-121">How to connect to a queue</span></span>

<span data-ttu-id="db113-122">若要连接到队列, 请首先`CloudStorageAccount`使用连接字符串创建。</span><span class="sxs-lookup"><span data-stu-id="db113-122">To connect to a queue, you first create a `CloudStorageAccount` with your connection string.</span></span> <span data-ttu-id="db113-123">然后`CloudQueueClient`, 生成的对象可以创建, 后者又可以打开`CloudQueue`实例。</span><span class="sxs-lookup"><span data-stu-id="db113-123">The resulting object can then create a `CloudQueueClient`, which in turn can open a `CloudQueue` instance.</span></span> <span data-ttu-id="db113-124">基本代码流如下所示。</span><span class="sxs-lookup"><span data-stu-id="db113-124">The basic code flow is shown below.</span></span>

```csharp
CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudQueueClient client = account.CreateCloudQueueClient();

CloudQueue queue = client.GetQueueReference("myqueue");
```

<span data-ttu-id="db113-125">创建的`CloudQueue`并不一定意味着_实际_存储队列存在。</span><span class="sxs-lookup"><span data-stu-id="db113-125">Creating a `CloudQueue` doesn't necessarily mean the _actual_ storage queue exists.</span></span> <span data-ttu-id="db113-126">但是, 可以使用此对象创建、删除和检查现有队列。</span><span class="sxs-lookup"><span data-stu-id="db113-126">However, you can use this object to create, delete, and check for an existing queue.</span></span> <span data-ttu-id="db113-127">如前所述, 所有方法都支持同步和异步版本, 但我们仅使用基于此的`Task`异步版本。</span><span class="sxs-lookup"><span data-stu-id="db113-127">As mentioned above, all methods support both synchronous and asynchronous versions, but we will only be using the `Task`-based asynchronous versions.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="db113-128">如何创建队列</span><span class="sxs-lookup"><span data-stu-id="db113-128">How to create a queue</span></span>

<span data-ttu-id="db113-129">将使用常见的队列创建模式: 发件人应用程序应始终负责创建队列。</span><span class="sxs-lookup"><span data-stu-id="db113-129">You will use a common pattern for queue creation: the sender application should always be responsible for creating the queue.</span></span> <span data-ttu-id="db113-130">这将使您的应用程序更独立且更不依赖于管理设置。</span><span class="sxs-lookup"><span data-stu-id="db113-130">This keeps your application more self-contained and less dependent on administrative set-up.</span></span> 

<span data-ttu-id="db113-131">若要简化创建过程, 客户端库会公开`CreateIfNotExistsAsync`创建队列的方法 (如有必要), 如果`false`队列已经存在, 则返回。</span><span class="sxs-lookup"><span data-stu-id="db113-131">To make the creation simple, the client library exposes a `CreateIfNotExistsAsync` method that will create the queue if necessary, or return `false` if the queue already exists.</span></span> 

<span data-ttu-id="db113-132">典型代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="db113-132">Typical code is shown below.</span></span>

```csharp
CloudQueue queue;
//...

await queue.CreateIfNotExistsAsync();
```

> [!NOTE]
> <span data-ttu-id="db113-133">您必须拥有`Write`存储`Create`帐户的或权限, 才能使用此 API。</span><span class="sxs-lookup"><span data-stu-id="db113-133">You must have `Write` or `Create` permissions for the storage account to use this API.</span></span> <span data-ttu-id="db113-134">如果使用**访问密钥**安全模型, 则始终为 true, 但可以使用将仅允许对队列进行读取操作的其他方法锁定对帐户的权限。</span><span class="sxs-lookup"><span data-stu-id="db113-134">This is always true if you use the **Access Key** security model, but you can lock down permissions to the account with other approaches that will only allow read operations against the queue.</span></span>

## <a name="how-to-send-a-message"></a><span data-ttu-id="db113-135">如何发送邮件</span><span class="sxs-lookup"><span data-stu-id="db113-135">How to send a message</span></span>

<span data-ttu-id="db113-136">若要发送邮件, 需要实例化`CloudQueueMessage`对象。</span><span class="sxs-lookup"><span data-stu-id="db113-136">To send a message, you instantiate a `CloudQueueMessage` object.</span></span> <span data-ttu-id="db113-137">类有几个重载构造函数, 用于将数据加载到邮件中。</span><span class="sxs-lookup"><span data-stu-id="db113-137">The class has a few overloaded constructors that load your data into the message.</span></span> <span data-ttu-id="db113-138">我们将使用采用的构造函数`string`。</span><span class="sxs-lookup"><span data-stu-id="db113-138">We will use the constructor that takes a `string`.</span></span> <span data-ttu-id="db113-139">创建邮件后, 使用`CloudQueue`对象发送该邮件。</span><span class="sxs-lookup"><span data-stu-id="db113-139">After creating the message, you use a `CloudQueue` object to send it.</span></span>

<span data-ttu-id="db113-140">下面是一个典型的示例:</span><span class="sxs-lookup"><span data-stu-id="db113-140">Here's a typical example:</span></span>

```csharp
var message = new CloudQueueMessage("your message here");

CloudQueue queue;
//...

await queue.AddMessageAsync(message);
```

> [!NOTE]
> <span data-ttu-id="db113-141">虽然队列总数最高可达 500 TB, 但其中的各个邮件的大小最大只能为 64 kb (使用 Base64 编码时的 48 KB)。</span><span class="sxs-lookup"><span data-stu-id="db113-141">While the total queue size can be up to 500 TB, the individual messages in it can only be up to 64 KB in size (48 KB when using Base64 encoding).</span></span> <span data-ttu-id="db113-142">如果需要更大的负载, 可以将队列和 blob 组合在一起, 将 URL 传递给邮件中的实际数据 (存储为 Blob)。</span><span class="sxs-lookup"><span data-stu-id="db113-142">If you need a larger payload you can combine queues and blobs – passing the URL to the actual data (stored as a Blob) in the message.</span></span> <span data-ttu-id="db113-143">利用此方法, 您可以将单个项目的排队设置为 200 GB。</span><span class="sxs-lookup"><span data-stu-id="db113-143">This approach would allow you to enqueue up to 200 GB for a single item.</span></span>

## <a name="how-to-receive-and-delete-a-message"></a><span data-ttu-id="db113-144">如何接收和删除邮件</span><span class="sxs-lookup"><span data-stu-id="db113-144">How to receive and delete a message</span></span>

<span data-ttu-id="db113-145">在接收器中, 您将获得下一封邮件, 进行处理, 然后在处理成功后将其删除。</span><span class="sxs-lookup"><span data-stu-id="db113-145">In the receiver, you get the next message, process it, and then delete it after processing succeeds.</span></span> <span data-ttu-id="db113-146">下面是一个简单的示例:</span><span class="sxs-lookup"><span data-stu-id="db113-146">Here's a simple example:</span></span>

```C#
CloudQueue queue;
//...

CloudQueueMessage message = await queue.GetMessageAsync();

if (message != null)
{
    // Process the message
    //...

    await queue.DeleteMessageAsync(message);
}
```

<span data-ttu-id="db113-147">现在让我们将此新知识应用到我们的应用程序!</span><span class="sxs-lookup"><span data-stu-id="db113-147">Let's now apply this new knowledge to our application!</span></span>