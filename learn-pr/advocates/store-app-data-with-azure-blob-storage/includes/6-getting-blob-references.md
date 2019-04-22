在 Azure 存储 SDK for .net Core 中使用单个 blob 需要*blob 引用* &mdash; `ICloudBlob`对象的实例。

您可以`ICloudBlob`通过使用 blob 的名称请求它, 或从容器中的 blob 列表中选择它来获取。 两者都需要`CloudBlobContainer`, 我们看到了如何获取最后一个单位。

## <a name="getting-blobs-by-name"></a>按名称获取 blob

调用上的`GetXXXReference`方法之一`CloudBlobContainer`可`ICloudBlob`按名称获取。 如果您知道要检索的 blob 的类型, 请使用特定的方法之一 (`GetBlockBlobReference`、 `GetAppendBlobReference`或`GetPageBlobReference`) 获取一个对象, 其中包含为该 blob 类型量身定制的方法和属性。

这些方法都不会进行网络调用, 也不会确认目标 blob 是否确实存在。 它们仅在本地创建 blob 引用对象, 该对象可用于调用在网络中*执行*操作并与存储区中的 blob 进行交互的方法。 一个单独的方法`GetBlobReferenceFromServerAsync`调用 blob 存储 API, 如果 blob 尚不存在, 则会引发异常。

## <a name="listing-blobs-in-a-container"></a>列出容器中的 blob

您可以使用`CloudBlobContainer`的`ListBlobsSegmentedAsync`方法获取容器中的 blob 列表。 *分段*指返回&mdash;一个单独调用的结果, `ListBlobsSegmentedAsync`并不保证在单个页面中返回所有结果。 我们可能需要使用它的`ContinuationToken`返回方式反复调用它, 以通过我们的页面进行工作。 这使得列出 blob 的代码比上载或下载代码更复杂, 但有一种标准模式可用于获取容器中的每个 blob:

```csharp
BlobContinuationToken continuationToken = null;
BlobResultSegment resultSegment = null;

do
{
    resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

    // Do work here on resultSegment.Results

    continuationToken = resultSegment.ContinuationToken;
} while (continuationToken != null);
```

这将重复`ListBlobsSegmentedAsync`调用, `continuationToken`直到`null`是, 这将指示结果的结束。

> [!IMPORTANT]
> 从不假定`ListBlobsSegmentedAsync`结果将到达单个页面。 始终检查延续令牌并使用它 (如果存在)。

### <a name="processing-list-results"></a>正在处理列表结果

您将返回的对象`ListBlobsSegmentedAsync`包含类型`Results` `IEnumerable<IListBlobItem>`的属性。 该`IListBlobItem`接口只包含有关 blob 的容器和 URL 的少数属性, 它本身并不十分有用。

若要从中获取有用的`Results`blob 对象, 可以使用`OfType<>`方法来筛选结果并将其转换为更具体的 blob 对象类型。 以下是几个示例:

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

> [!TIP]
> 使用`OfType<>`需要引用`System.Linq`命名空间 (`using System.Linq;`)。

## <a name="exercise"></a>健身

我们的应用程序中的功能之一需要获取 API 中的 blob 列表。 我们将使用上面显示的模式列出容器中的所有 blob。 在我们处理列表时, 我们会获取每个 blob 的名称。

使用编辑器, 将替换`GetNames`为`BlobStorage.cs`以下代码并保存所做的更改。

```csharp
public async Task<IEnumerable<string>> GetNames()
{
    List<string> names = new List<string>();

    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);

    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    do
    {
        resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

        // Get the name of each blob.
        names.AddRange(resultSegment.Results.OfType<ICloudBlob>().Select(b => b.Name));

        continuationToken = resultSegment.ContinuationToken;
    } while (continuationToken != null);

    return names;
}
```

> [!TIP]
> 请注意, 现在需要指定`async`方法签名。

此方法返回的名称将由`FilesController`进行处理, 以将其转换为 url。 当它们返回到客户端时, 它们将在页面上呈现为超链接。