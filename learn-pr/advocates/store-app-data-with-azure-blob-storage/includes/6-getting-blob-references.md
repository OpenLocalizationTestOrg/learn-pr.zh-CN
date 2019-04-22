<span data-ttu-id="37725-101">在 Azure 存储 SDK for .net Core 中使用单个 blob 需要*blob 引用* &mdash; `ICloudBlob`对象的实例。</span><span class="sxs-lookup"><span data-stu-id="37725-101">Working with an individual blob in the Azure Storage SDK for .NET Core requires a *blob reference* &mdash; an instance of an `ICloudBlob` object.</span></span>

<span data-ttu-id="37725-102">您可以`ICloudBlob`通过使用 blob 的名称请求它, 或从容器中的 blob 列表中选择它来获取。</span><span class="sxs-lookup"><span data-stu-id="37725-102">You can get an `ICloudBlob` by requesting it with the blob's name or selecting it from a list of blobs in the container.</span></span> <span data-ttu-id="37725-103">两者都需要`CloudBlobContainer`, 我们看到了如何获取最后一个单位。</span><span class="sxs-lookup"><span data-stu-id="37725-103">Both require a `CloudBlobContainer`, which we saw how to get in the last unit.</span></span>

## <a name="getting-blobs-by-name"></a><span data-ttu-id="37725-104">按名称获取 blob</span><span class="sxs-lookup"><span data-stu-id="37725-104">Getting blobs by name</span></span>

<span data-ttu-id="37725-105">调用上的`GetXXXReference`方法之一`CloudBlobContainer`可`ICloudBlob`按名称获取。</span><span class="sxs-lookup"><span data-stu-id="37725-105">Call one of the `GetXXXReference` methods on a `CloudBlobContainer` to get an `ICloudBlob` by name.</span></span> <span data-ttu-id="37725-106">如果您知道要检索的 blob 的类型, 请使用特定的方法之一 (`GetBlockBlobReference`、 `GetAppendBlobReference`或`GetPageBlobReference`) 获取一个对象, 其中包含为该 blob 类型量身定制的方法和属性。</span><span class="sxs-lookup"><span data-stu-id="37725-106">If you know the type of the blob you are retrieving, use one of the specific methods (`GetBlockBlobReference`, `GetAppendBlobReference`, or `GetPageBlobReference`) to get an object that includes methods and properties tailored for that blob type.</span></span>

<span data-ttu-id="37725-107">这些方法都不会进行网络调用, 也不会确认目标 blob 是否确实存在。</span><span class="sxs-lookup"><span data-stu-id="37725-107">None of these methods make network calls, nor do they confirm whether or not the targeted blob actually exists.</span></span> <span data-ttu-id="37725-108">它们仅在本地创建 blob 引用对象, 该对象可用于调用在网络中*执行*操作并与存储区中的 blob 进行交互的方法。</span><span class="sxs-lookup"><span data-stu-id="37725-108">They only create a blob reference object locally, which can then be used to call methods that *do* operate over the network and interact with blobs in storage.</span></span> <span data-ttu-id="37725-109">一个单独的方法`GetBlobReferenceFromServerAsync`调用 blob 存储 API, 如果 blob 尚不存在, 则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="37725-109">A separate method, `GetBlobReferenceFromServerAsync`, does call the Blob storage API and will throw an exception if the blob doesn't already exist.</span></span>

## <a name="listing-blobs-in-a-container"></a><span data-ttu-id="37725-110">列出容器中的 blob</span><span class="sxs-lookup"><span data-stu-id="37725-110">Listing blobs in a container</span></span>

<span data-ttu-id="37725-111">您可以使用`CloudBlobContainer`的`ListBlobsSegmentedAsync`方法获取容器中的 blob 列表。</span><span class="sxs-lookup"><span data-stu-id="37725-111">You can get a list of the blobs in a container using `CloudBlobContainer`'s `ListBlobsSegmentedAsync` method.</span></span> <span data-ttu-id="37725-112">*分段*指返回&mdash;一个单独调用的结果, `ListBlobsSegmentedAsync`并不保证在单个页面中返回所有结果。</span><span class="sxs-lookup"><span data-stu-id="37725-112">*Segmented* refers to the separate pages of results returned &mdash; a single call to `ListBlobsSegmentedAsync` is never guaranteed to return all the results in a single page.</span></span> <span data-ttu-id="37725-113">我们可能需要使用它的`ContinuationToken`返回方式反复调用它, 以通过我们的页面进行工作。</span><span class="sxs-lookup"><span data-stu-id="37725-113">We may need to call it repeatedly using the `ContinuationToken` it returns to work our way through the pages.</span></span> <span data-ttu-id="37725-114">这使得列出 blob 的代码比上载或下载代码更复杂, 但有一种标准模式可用于获取容器中的每个 blob:</span><span class="sxs-lookup"><span data-stu-id="37725-114">This makes the code for listing blobs a little more complex than the code for uploading or downloading, but there's a standard pattern you can use to get every blob in a container:</span></span>

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

<span data-ttu-id="37725-115">这将重复`ListBlobsSegmentedAsync`调用, `continuationToken`直到`null`是, 这将指示结果的结束。</span><span class="sxs-lookup"><span data-stu-id="37725-115">This will call `ListBlobsSegmentedAsync` repeatedly until `continuationToken` is `null`, which signals the end of the results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37725-116">从不假定`ListBlobsSegmentedAsync`结果将到达单个页面。</span><span class="sxs-lookup"><span data-stu-id="37725-116">Never assume that `ListBlobsSegmentedAsync` results will arrive in a single page.</span></span> <span data-ttu-id="37725-117">始终检查延续令牌并使用它 (如果存在)。</span><span class="sxs-lookup"><span data-stu-id="37725-117">Always check for a continuation token and use it if it's present.</span></span>

### <a name="processing-list-results"></a><span data-ttu-id="37725-118">正在处理列表结果</span><span class="sxs-lookup"><span data-stu-id="37725-118">Processing list results</span></span>

<span data-ttu-id="37725-119">您将返回的对象`ListBlobsSegmentedAsync`包含类型`Results` `IEnumerable<IListBlobItem>`的属性。</span><span class="sxs-lookup"><span data-stu-id="37725-119">The object you'll get back from `ListBlobsSegmentedAsync` contains a `Results` property of type `IEnumerable<IListBlobItem>`.</span></span> <span data-ttu-id="37725-120">该`IListBlobItem`接口只包含有关 blob 的容器和 URL 的少数属性, 它本身并不十分有用。</span><span class="sxs-lookup"><span data-stu-id="37725-120">The `IListBlobItem` interface includes only a handful of properties about the blob's container and URL, and isn't very useful by itself.</span></span>

<span data-ttu-id="37725-121">若要从中获取有用的`Results`blob 对象, 可以使用`OfType<>`方法来筛选结果并将其转换为更具体的 blob 对象类型。</span><span class="sxs-lookup"><span data-stu-id="37725-121">To get useful blob objects out of `Results`, you can use the `OfType<>` method to filter and cast the results to more specific blob object types.</span></span> <span data-ttu-id="37725-122">以下是几个示例:</span><span class="sxs-lookup"><span data-stu-id="37725-122">Here are a few examples:</span></span>

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

> [!TIP]
> <span data-ttu-id="37725-123">使用`OfType<>`需要引用`System.Linq`命名空间 (`using System.Linq;`)。</span><span class="sxs-lookup"><span data-stu-id="37725-123">Using `OfType<>` requires a reference to the `System.Linq` namespace (`using System.Linq;`).</span></span>

## <a name="exercise"></a><span data-ttu-id="37725-124">健身</span><span class="sxs-lookup"><span data-stu-id="37725-124">Exercise</span></span>

<span data-ttu-id="37725-125">我们的应用程序中的功能之一需要获取 API 中的 blob 列表。</span><span class="sxs-lookup"><span data-stu-id="37725-125">One of the features in our app requires getting a list of blobs from the API.</span></span> <span data-ttu-id="37725-126">我们将使用上面显示的模式列出容器中的所有 blob。</span><span class="sxs-lookup"><span data-stu-id="37725-126">We'll use the pattern shown above to list all the blobs in our container.</span></span> <span data-ttu-id="37725-127">在我们处理列表时, 我们会获取每个 blob 的名称。</span><span class="sxs-lookup"><span data-stu-id="37725-127">As we process the list, we get the name of each blob.</span></span>

<span data-ttu-id="37725-128">使用编辑器, 将替换`GetNames`为`BlobStorage.cs`以下代码并保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="37725-128">Using the editor, replace `GetNames` in `BlobStorage.cs` with the following code and save your changes.</span></span>

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
> <span data-ttu-id="37725-129">请注意, 现在需要指定`async`方法签名。</span><span class="sxs-lookup"><span data-stu-id="37725-129">Note that the method signature now needs to specify `async`.</span></span>

<span data-ttu-id="37725-130">此方法返回的名称将由`FilesController`进行处理, 以将其转换为 url。</span><span class="sxs-lookup"><span data-stu-id="37725-130">The names returned by this method are processed by `FilesController` to turn them into URLs.</span></span> <span data-ttu-id="37725-131">当它们返回到客户端时, 它们将在页面上呈现为超链接。</span><span class="sxs-lookup"><span data-stu-id="37725-131">When they are returned to the client, they are rendered as hyperlinks on the page.</span></span>