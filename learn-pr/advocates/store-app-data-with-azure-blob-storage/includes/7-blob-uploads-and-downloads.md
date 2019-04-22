<span data-ttu-id="a0e29-101">有了对 blob 的引用后, 即可上载和下载数据。</span><span class="sxs-lookup"><span data-stu-id="a0e29-101">Once we have a reference to a blob, we can upload and download data.</span></span> <span data-ttu-id="a0e29-102">`ICloudBlob`对象具有`Upload`支持`Download`作为源和目标的字节数组、流和文件的方法和方法。</span><span class="sxs-lookup"><span data-stu-id="a0e29-102">`ICloudBlob` objects have `Upload` and `Download` methods that support byte arrays, streams, and files as sources and targets.</span></span> <span data-ttu-id="a0e29-103">特定类型具有&mdash;更多方便的方法, 例如`CloudBlockBlob` , 支持使用和`UploadTextAsync` `DownloadTextAsync`在上传和下载字符串。</span><span class="sxs-lookup"><span data-stu-id="a0e29-103">Specific types have additional methods for convenience &mdash; for example, `CloudBlockBlob` supports uploading and downloading strings with `UploadTextAsync` and `DownloadTextAsync`.</span></span>

## <a name="creating-new-blobs"></a><span data-ttu-id="a0e29-104">创建新的 blob</span><span class="sxs-lookup"><span data-stu-id="a0e29-104">Creating new blobs</span></span>

<span data-ttu-id="a0e29-105">若要创建新的 blob, 请调用对存储`Upload`中不存在的 blob 的引用的方法之一。</span><span class="sxs-lookup"><span data-stu-id="a0e29-105">To create a new blob, you call one of the `Upload` methods on a reference to a blob that doesn't exist in storage.</span></span> <span data-ttu-id="a0e29-106">这将执行两项操作: 在存储区中创建 blob 并上载数据。</span><span class="sxs-lookup"><span data-stu-id="a0e29-106">This does two things: creates the blob in storage and uploads the data.</span></span>

## <a name="moving-data-to-and-from-blobs"></a><span data-ttu-id="a0e29-107">在 blob 之间移动数据</span><span class="sxs-lookup"><span data-stu-id="a0e29-107">Moving data to and from blobs</span></span>

<span data-ttu-id="a0e29-108">在 blob 之间移动数据是一种需要花费时间的网络操作。</span><span class="sxs-lookup"><span data-stu-id="a0e29-108">Moving data to and from a blob is a network operation that takes time.</span></span> <span data-ttu-id="a0e29-109">在适用于 .net Core 的 Azure 存储 SDK 中, 所有需要网络活动返回`Task`的方法, 因此请确保正确`await`地在控制器方法中使用。</span><span class="sxs-lookup"><span data-stu-id="a0e29-109">In the Azure Storage SDK for .NET Core, all methods that require network activity return `Task`s, so make sure you use `await` in your controller methods appropriately.</span></span>

<span data-ttu-id="a0e29-110">处理大型数据对象时的一个常见建议是使用流, 而不是内存中的结构, 如字节数组或字符串。</span><span class="sxs-lookup"><span data-stu-id="a0e29-110">A common recommendation when working with large data objects is to use streams instead of in-memory structures like byte arrays or strings.</span></span> <span data-ttu-id="a0e29-111">这样可避免在将完整内容发送到目标之前对内存中的内容进行缓冲。</span><span class="sxs-lookup"><span data-stu-id="a0e29-111">This avoids buffering the full content in memory before sending it to the target.</span></span> <span data-ttu-id="a0e29-112">ASP.NET Core 支持从请求和响应读取和写入流。</span><span class="sxs-lookup"><span data-stu-id="a0e29-112">ASP.NET Core supports reading and writing streams from requests and responses.</span></span>

## <a name="concurrent-access"></a><span data-ttu-id="a0e29-113">并发访问</span><span class="sxs-lookup"><span data-stu-id="a0e29-113">Concurrent access</span></span>

<span data-ttu-id="a0e29-114">当您的应用程序正在使用时, 其他进程可能会添加、更改或删除 blob。</span><span class="sxs-lookup"><span data-stu-id="a0e29-114">Other processes may be adding, changing, or deleting blobs as your app is using them.</span></span> <span data-ttu-id="a0e29-115">始终对 defensively 进行编码并考虑由并发导致的问题, 例如, 在您尝试从这些文件中下载时被删除的 blob, 或者在您不希望其内容发生更改的 blob。</span><span class="sxs-lookup"><span data-stu-id="a0e29-115">Always code defensively and think about problems caused by concurrency, such as blobs that are deleted right as you try to download from them, or blobs whose contents change when you don't expect them to.</span></span> <span data-ttu-id="a0e29-116">有关使用 AccessConditions 和 blob 租用管理并发 blob 访问的信息, 请参阅本模块结尾的其他阅读部分。</span><span class="sxs-lookup"><span data-stu-id="a0e29-116">See the Further Reading section at the end of this module for information about using AccessConditions and blob leases to manage concurrent blob access.</span></span>

## <a name="exercise"></a><span data-ttu-id="a0e29-117">健身</span><span class="sxs-lookup"><span data-stu-id="a0e29-117">Exercise</span></span>

<span data-ttu-id="a0e29-118">让我们通过添加上载和下载代码来完成应用, 然后将其部署到 Azure 应用服务进行测试。</span><span class="sxs-lookup"><span data-stu-id="a0e29-118">Let's finish our app by adding upload and download code, then deploy it to Azure App Service for testing.</span></span>

### <a name="upload"></a><span data-ttu-id="a0e29-119">[</span><span class="sxs-lookup"><span data-stu-id="a0e29-119">Upload</span></span>

<span data-ttu-id="a0e29-120">若要上传 blob, 我们将实现`BlobStorage.Save`使用`GetBlockBlobReference`从容器获取的`CloudBlockBlob`方法。</span><span class="sxs-lookup"><span data-stu-id="a0e29-120">To upload a blob, we'll implement the `BlobStorage.Save` method using `GetBlockBlobReference` to get a `CloudBlockBlob` from the container.</span></span> <span data-ttu-id="a0e29-121">`FilesController.Upload`将文件流传递给`Save`, 以便我们可以使用`UploadFromStreamAsync`执行上载以实现最大效率。</span><span class="sxs-lookup"><span data-stu-id="a0e29-121">`FilesController.Upload` passes the file stream to `Save`, so we can use `UploadFromStreamAsync` to perform the upload for maximum efficiency.</span></span>

<span data-ttu-id="a0e29-122">在编辑器中, 将`Save`替换`BlobStorage.cs`为以下代码:</span><span class="sxs-lookup"><span data-stu-id="a0e29-122">In the editor, replace `Save` in `BlobStorage.cs` with the following code:</span></span>

```csharp
public Task Save(Stream fileStream, string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
    return blockBlob.UploadFromStreamAsync(fileStream);
}
```

> [!NOTE]
> <span data-ttu-id="a0e29-123">此处显示的基于流的上载代码比在将文件发送到 Azure Blob 存储之前将文件读取到字节数组中的效率更高。</span><span class="sxs-lookup"><span data-stu-id="a0e29-123">The stream-based upload code shown here is more efficient than reading the file into a byte array before sending it to Azure Blob storage.</span></span> <span data-ttu-id="a0e29-124">但是, 我们用来`IFormFile`从客户端获取文件的 ASP.NET 核心技术并不是真正的端到端流实现, 仅适用于处理小文件的上载。</span><span class="sxs-lookup"><span data-stu-id="a0e29-124">However, the ASP.NET Core `IFormFile` technique we use to get the file from the client is not a true end-to-end streaming implementation and is only appropriate for handling uploads of small files.</span></span> <span data-ttu-id="a0e29-125">有关完全流式文件上载的信息, 请参阅本模块结尾的进一步阅读部分。</span><span class="sxs-lookup"><span data-stu-id="a0e29-125">See the Further Reading section at the end of this module for information about fully streamed file uploads.</span></span>

### <a name="download"></a><span data-ttu-id="a0e29-126">下载</span><span class="sxs-lookup"><span data-stu-id="a0e29-126">Download</span></span>

<span data-ttu-id="a0e29-127">`BlobStorage.Load`返回一个`Stream`, 意味着我们的代码不需要实际移动 blob 存储&mdash;中的字节, 只需返回对 blob 流的引用。</span><span class="sxs-lookup"><span data-stu-id="a0e29-127">`BlobStorage.Load` returns a `Stream`, meaning that our code doesn't need to physically move the bytes from Blob storage at all &mdash; we just need to return a reference to the blob stream.</span></span> <span data-ttu-id="a0e29-128">可以使用`OpenReadAsync`来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="a0e29-128">We can do that with `OpenReadAsync`.</span></span> <span data-ttu-id="a0e29-129">ASP.NET 核心将在生成客户端响应时处理读取和关闭流。</span><span class="sxs-lookup"><span data-stu-id="a0e29-129">ASP.NET Core will handle reading and closing the stream when it builds the client response.</span></span>

<span data-ttu-id="a0e29-130">将`Load`替换为此代码并保存您的工作:</span><span class="sxs-lookup"><span data-stu-id="a0e29-130">Replace `Load` with this code and save your work:</span></span>

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a><span data-ttu-id="a0e29-131">在 Azure 中部署和运行</span><span class="sxs-lookup"><span data-stu-id="a0e29-131">Deploy and run in Azure</span></span>

<span data-ttu-id="a0e29-132">我们的应用程序&mdash;已完成, 让我们对其进行部署, 并查看它能否正常工作。</span><span class="sxs-lookup"><span data-stu-id="a0e29-132">Our app is finished &mdash; let's deploy it and see it work.</span></span> <span data-ttu-id="a0e29-133">使用存储帐户连接字符串和容器名称的应用程序设置创建 app Service 应用并对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="a0e29-133">Create an App Service app and configure it with application settings for our storage account connection string and container name.</span></span> <span data-ttu-id="a0e29-134">获取存储帐户的连接字符串`az storage account show-connection-string` , 并将容器的名称设置为。 `files`</span><span class="sxs-lookup"><span data-stu-id="a0e29-134">Get the storage account's connection string with `az storage account show-connection-string` and set the name of the container to be `files`.</span></span>

<span data-ttu-id="a0e29-135">应用名称必须是全局唯一的, 因此需要选择自己的`<your-unique-app-name>`名称以进行填写。</span><span class="sxs-lookup"><span data-stu-id="a0e29-135">The app name needs to be globally unique, so you'll need to choose your own name to fill in `<your-unique-app-name>`.</span></span>

```azurecli
az appservice plan create --name blob-exercise-plan --resource-group <rgn>[sandbox resource group name]</rgn>
az webapp create --name <your-unique-app-name> --plan blob-exercise-plan --resource-group <rgn>[sandbox resource group name]</rgn>
CONNECTIONSTRING=$(az storage account show-connection-string --name <your-unique-storage-account-name> --output tsv)
az webapp config appsettings set --name <your-unique-app-name> --resource-group <rgn>[sandbox resource group name]</rgn> --settings AzureStorageConfig:ConnectionString=$CONNECTIONSTRING AzureStorageConfig:FileContainerName=files
```

<span data-ttu-id="a0e29-136">现在我们将部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0e29-136">Now we'll deploy our app.</span></span> <span data-ttu-id="a0e29-137">下面的命令将网站发布到`pub`文件夹, 将其压缩到`site.zip`, 并将 zip 部署到 App Service。</span><span class="sxs-lookup"><span data-stu-id="a0e29-137">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="a0e29-138">运行以下命令之前, 请确保您`mslearn-store-data-in-azure/store-app-data-with-azure-blob-storage/src/start`的命令行管理程序仍在目录中。</span><span class="sxs-lookup"><span data-stu-id="a0e29-138">Make sure your shell is still in the `mslearn-store-data-in-azure/store-app-data-with-azure-blob-storage/src/start` directory before running the following commands.</span></span>

```azurecli
dotnet publish -o pub
cd pub
zip -r ../site.zip *
az webapp deployment source config-zip --src ../site.zip --name <your-unique-app-name> --resource-group <rgn>[sandbox resource group name]</rgn>
```

<span data-ttu-id="a0e29-139">在`https://<your-unique-app-name>.azurewebsites.net`浏览器中打开以查看正在运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0e29-139">Open `https://<your-unique-app-name>.azurewebsites.net` in a browser to see the running app.</span></span> <span data-ttu-id="a0e29-140">其外观应如下图所示。</span><span class="sxs-lookup"><span data-stu-id="a0e29-140">It should look like the image below.</span></span>

![FileUploader web 应用程序的屏幕截图](../media/7-fileuploader-empty.PNG)

<span data-ttu-id="a0e29-142">尝试上载并下载一些文件以测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0e29-142">Try uploading and downloading some files to test the app.</span></span> <span data-ttu-id="a0e29-143">上载一些文件后, 请在命令行管理程序中运行以下命令, 以查看已上载到容器的 blob:</span><span class="sxs-lookup"><span data-stu-id="a0e29-143">After you've uploaded a few files, run the following in the shell to see the blobs that have been uploaded to the container:</span></span>

```console
az storage blob list --account-name <your-unique-storage-account-name> --container-name files --query [].{Name:name} --output table
```