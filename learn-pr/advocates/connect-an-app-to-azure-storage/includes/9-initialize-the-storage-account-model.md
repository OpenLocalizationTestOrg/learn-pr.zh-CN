azure 存储客户端库提供了一个用于与 Azure 存储帐户进行交互的对象模型。 它用于快速连接到 azure 存储帐户并使用 azure 存储服务 api。 

## <a name="azure-storage-client-library-object-model"></a>Azure 存储客户端库对象模型

::: zone pivot="csharp"

.net Core 客户端库中存储帐户对象模型的基础是类`CloudStorageAccount`。 初始化对象模型的最简单方法是使用`CloudStorageAccount.Parse`或`CloudStorageAccount.TryParse`分析连接字符串。

> [!NOTE]
> 在调用需要的操作之前, 客户端库不会尝试连接。 `Parse()``TryParse()`仅确保连接字符串格式正确;他们不会验证帐户是否存在, 或者密钥是否正确。 

从`CloudStorageAccount` `Parse()` or `TryParse()`方法调用返回的结果实例将公开用于创建客户端对象以访问 Azure Blob、文件、队列和表存储服务的方法。 

下面的代码段显示了创建用于 blob 存储的客户端的示例:

```csharp
using Microsoft.WindowsAzure.Storage;

CloudStorageAccount storageAccount = CloudStorageAccount.Parse("your-storage-key-connection-string");

CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

`CloudStorageAccount`客户端对象是轻型的, 并且可以根据需要创建, 也可以在应用程序中共享之前创建。 一种标准方法是在`CloudStorageAccount.TryParse()`应用程序的入口点附近创建一个实例, 并使其在应用程序中可用于创建客户端实例。

将客户端对象提供给特定的存储类型后, 您可以使用方法执行实际工作。 在 .net 中特意异步&mdash;进行网络调用的方法我们使用`async`和`await`关键字来有效地处理这些方法。

例如, 我们可以使用`CloudBlobClient`创建_blob 容器_并将文件上传到 blob 存储。

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

**node.js 和 JavaScript 的 Microsoft Azure 存储客户端库**中的存储帐户对象模型的基础是`azurestorage`对象。 这是通过`require`语句将**azure 存储**模块添加到应用中创建的。

```javascript
const storage = require('azure-storage');
```

此对象提供了一系列_工厂_方法, 这些方法创建特定对象以使用 Azure 存储的每个层面。 调用`createXXX`方法以创建每个对象。

| 类型 | 方法 | 返回 |
|--------|---------|-------------|
| **块** | `createBlobService` | `BlobService` |
| **Table** | `createTableService` | `TableService` |
| **列队** | `createQueueService` | `QueueService` |
| **文件** | `createFileService` | `FileService` |

> [!NOTE]
> 在调用需要的操作之前, 客户端库不会尝试连接。 这些`create`方法中的每一个都返回一个轻量级对象, 该对象&mdash;表示对存储类型的访问不验证所使用的连接或访问键。

将服务对象提供给特定的存储类型后, 您可以使用方法执行实际工作。 进行网络调用的方法是特意异步进行的。 库当前支持_回调_以返回异步结果。 例如, 下面是创建 blob 容器的代码。

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

这种方法可以正常运行, 但会导致在回调中添加大量代码, 这可能会导致无法控制。 JavaScript 中的一种更好的方法是使用_承诺_来处理这些方法。 有几个大库会将回叫样式的方法转换为&mdash;承诺, 您可以选取您喜欢的方法。

在这里, 我们将使用`util.promisify`节点中的功能, 并`BlobService`使用创建容器并将文件上传到 blob 存储。 此外, 我们还将使用`async`和`await`关键字来更自然地处理承诺。

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

让我们在应用中尝试一下。