<span data-ttu-id="b8c0a-101">azure 存储客户端库提供了一个用于与 Azure 存储帐户进行交互的对象模型。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-101">The Azure Storage client library provides an object model that is used to interact with Azure storage accounts.</span></span> <span data-ttu-id="b8c0a-102">它用于快速连接到 azure 存储帐户并使用 azure 存储服务 api。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-102">It's used to quickly connect to an Azure storage account and use the Azure Storage service APIs.</span></span> 

## <a name="azure-storage-client-library-object-model"></a><span data-ttu-id="b8c0a-103">Azure 存储客户端库对象模型</span><span class="sxs-lookup"><span data-stu-id="b8c0a-103">Azure Storage client library object model</span></span>

::: zone pivot="csharp"

<span data-ttu-id="b8c0a-104">.net Core 客户端库中存储帐户对象模型的基础是类`CloudStorageAccount`。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-104">The foundation of the storage account object model in the .NET Core client library is the class `CloudStorageAccount`.</span></span> <span data-ttu-id="b8c0a-105">初始化对象模型的最简单方法是使用`CloudStorageAccount.Parse`或`CloudStorageAccount.TryParse`分析连接字符串。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-105">The simplest way to initialize the object model is to use `CloudStorageAccount.Parse` or `CloudStorageAccount.TryParse` to parse the connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="b8c0a-106">在调用需要的操作之前, 客户端库不会尝试连接。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-106">The client library will not attempt to connect until an operation is invoked that requires it.</span></span> <span data-ttu-id="b8c0a-107">`Parse()``TryParse()`仅确保连接字符串格式正确;他们不会验证帐户是否存在, 或者密钥是否正确。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-107">`Parse()` and `TryParse()` only guarantee that the connection string is well-formatted; they don't verify that the account exists or that the key is correct.</span></span> 

<span data-ttu-id="b8c0a-108">从`CloudStorageAccount` `Parse()` or `TryParse()`方法调用返回的结果实例将公开用于创建客户端对象以访问 Azure Blob、文件、队列和表存储服务的方法。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-108">The resulting `CloudStorageAccount` instance returned from the `Parse()` or `TryParse()` method call exposes methods to create a client objects to access the Azure Blob, Files, Queue and Table storage services.</span></span> 

<span data-ttu-id="b8c0a-109">下面的代码段显示了创建用于 blob 存储的客户端的示例:</span><span class="sxs-lookup"><span data-stu-id="b8c0a-109">The code snippet below shows an example of creating a client to use for blob storage:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;

CloudStorageAccount storageAccount = CloudStorageAccount.Parse("your-storage-key-connection-string");

CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="b8c0a-110">`CloudStorageAccount`客户端对象是轻型的, 并且可以根据需要创建, 也可以在应用程序中共享之前创建。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-110">`CloudStorageAccount` and the client objects are lightweight and can be created on demand or created up front to be shared within your application.</span></span> <span data-ttu-id="b8c0a-111">一种标准方法是在`CloudStorageAccount.TryParse()`应用程序的入口点附近创建一个实例, 并使其在应用程序中可用于创建客户端实例。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-111">A standard approach is to use `CloudStorageAccount.TryParse()` near the entry point of your application to create an instance, and make it available within your application for creating client instances.</span></span>

<span data-ttu-id="b8c0a-112">将客户端对象提供给特定的存储类型后, 您可以使用方法执行实际工作。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-112">Once you have a client object to a specific storage type, you can use methods to perform actual work.</span></span> <span data-ttu-id="b8c0a-113">在 .net 中特意异步&mdash;进行网络调用的方法我们使用`async`和`await`关键字来有效地处理这些方法。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-113">Methods which make network calls are intentionally asynchronous &mdash; in .NET we use the `async` and `await` keywords to work with these methods efficiently.</span></span>

<span data-ttu-id="b8c0a-114">例如, 我们可以使用`CloudBlobClient`创建_blob 容器_并将文件上传到 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-114">As an example, we can use the `CloudBlobClient` to create a _blob container_ and upload a file to blob storage.</span></span>

```csharp
// Create a local CloudBlobContainer object. No network call.
string containerName = "myblobcontainer";
CloudBlobContainer blobContainer = blobClient.GetContainerReference(containerName);

// This makes an actual service call to the Azure Storage service. 
// Unless this call fails, the container will have been created.
await blobContainer.CreateAsync();

// Create a local object to represent our blob. No network call.
string blobName = "myphoto";
CloudBlockBlob blob = blobContainer.GetBlockBlobReference(blobName);

// This transfers data in the file to the blob on the service.
string filename = "photo.png";
await blob.UploadFromFileAsync(fileName);
```

::: zone-end

::: zone pivot="javascript"

<span data-ttu-id="b8c0a-115">**node.js 和 JavaScript 的 Microsoft Azure 存储客户端库**中的存储帐户对象模型的基础是`azurestorage`对象。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-115">The foundation of the storage account object model in the **Microsoft Azure Storage Client Library for Node.js and JavaScript** is the `azurestorage` object.</span></span> <span data-ttu-id="b8c0a-116">这是通过`require`语句将**azure 存储**模块添加到应用中创建的。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-116">This is created by adding the **azure-storage** module to your app through a `require` statement.</span></span>

```javascript
const storage = require('azure-storage');
```

<span data-ttu-id="b8c0a-117">此对象提供了一系列_工厂_方法, 这些方法创建特定对象以使用 Azure 存储的每个层面。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-117">This object provides a series of _factory_ methods that create specific objects to work with each facet of Azure storage.</span></span> <span data-ttu-id="b8c0a-118">调用`createXXX`方法以创建每个对象。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-118">You call `createXXX` methods to create each object.</span></span>

| <span data-ttu-id="b8c0a-119">类型</span><span class="sxs-lookup"><span data-stu-id="b8c0a-119">Type</span></span> | <span data-ttu-id="b8c0a-120">方法</span><span class="sxs-lookup"><span data-stu-id="b8c0a-120">Method</span></span> | <span data-ttu-id="b8c0a-121">返回</span><span class="sxs-lookup"><span data-stu-id="b8c0a-121">Returns</span></span> |
|--------|---------|-------------|
| <span data-ttu-id="b8c0a-122">**块**</span><span class="sxs-lookup"><span data-stu-id="b8c0a-122">**Blob**</span></span> | `createBlobService` | `BlobService` |
| <span data-ttu-id="b8c0a-123">**Table**</span><span class="sxs-lookup"><span data-stu-id="b8c0a-123">**Table**</span></span> | `createTableService` | `TableService` |
| <span data-ttu-id="b8c0a-124">**列队**</span><span class="sxs-lookup"><span data-stu-id="b8c0a-124">**Queue**</span></span> | `createQueueService` | `QueueService` |
| <span data-ttu-id="b8c0a-125">**文件**</span><span class="sxs-lookup"><span data-stu-id="b8c0a-125">**File**</span></span> | `createFileService` | `FileService` |

> [!NOTE]
> <span data-ttu-id="b8c0a-126">在调用需要的操作之前, 客户端库不会尝试连接。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-126">The client library will not attempt to connect until an operation is invoked that requires it.</span></span> <span data-ttu-id="b8c0a-127">这些`create`方法中的每一个都返回一个轻量级对象, 该对象&mdash;表示对存储类型的访问不验证所使用的连接或访问键。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-127">Each of these `create` methods return a lightweight object representing access to the storage type&mdash;it does not validate the connection or the access key being used.</span></span>

<span data-ttu-id="b8c0a-128">将服务对象提供给特定的存储类型后, 您可以使用方法执行实际工作。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-128">Once you have a service object to a specific storage type, you can use methods to perform actual work.</span></span> <span data-ttu-id="b8c0a-129">进行网络调用的方法是特意异步进行的。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-129">Methods that make network calls are intentionally asynchronous.</span></span> <span data-ttu-id="b8c0a-130">库当前支持_回调_以返回异步结果。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-130">The library currently supports _callbacks_ to return asynchronous results.</span></span> <span data-ttu-id="b8c0a-131">例如, 下面是创建 blob 容器的代码。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-131">For example, here is code that creates a blob container.</span></span>

```javascript
var azure = require('azure-storage');
var blobService = azure.createBlobService();

blobService.createContainerIfNotExists('myblobcontainer', function(err, result, response) {
  if (!err) {
    // if result.created = true, container was created.
    // if result.created = false, container already existed.
  }
});
```

<span data-ttu-id="b8c0a-132">这种方法可以正常运行, 但会导致在回调中添加大量代码, 这可能会导致无法控制。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-132">This approach works fine, but it tends to lead to a lot of code being added into the callbacks, which can get unmanageable.</span></span> <span data-ttu-id="b8c0a-133">JavaScript 中的一种更好的方法是使用_承诺_来处理这些方法。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-133">A better approach in JavaScript is to use _promises_ to work with these methods.</span></span> <span data-ttu-id="b8c0a-134">有几个大库会将回叫样式的方法转换为&mdash;承诺, 您可以选取您喜欢的方法。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-134">There are several great libraries which will convert callback-style methods into promises&mdash;you can pick the one you prefer.</span></span>

<span data-ttu-id="b8c0a-135">在这里, 我们将使用`util.promisify`节点中的功能, 并`BlobService`使用创建容器并将文件上传到 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-135">Here, we'll use the `util.promisify` feature from Node and use the `BlobService` to create the container and upload a file to blob storage.</span></span> <span data-ttu-id="b8c0a-136">此外, 我们还将使用`async`和`await`关键字来更自然地处理承诺。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-136">In addition, we'll use the `async` and `await` keywords to work with the promises a bit more naturally.</span></span>

```javascript
const util = require('util');
const storage = require('azure-storage');

const blobService = storage.createBlobService();
const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);
const uploadBlobAsync = util.promisify(blobService.createBlockBlobFromLocalFile).bind(blobService);

async function main() {
    try {
        // This makes an actual service call to the Azure Storage service. 
        // Unless this call fails, the container will have been created.
        await createContainerAsync(containerName);

        // This transfers data in the file to the blob on the service.
        var uploadResult = await uploadBlobAsync(containerName, "myphoto", "photo.png");
        if (uploadResult) {
            console.log("blob uploaded");
        }
    }
    catch (err) {
        console.log(err.message);
    }
}

main();
```
::: zone-end

<span data-ttu-id="b8c0a-137">让我们在应用中尝试一下。</span><span class="sxs-lookup"><span data-stu-id="b8c0a-137">Let's try this in our app.</span></span>