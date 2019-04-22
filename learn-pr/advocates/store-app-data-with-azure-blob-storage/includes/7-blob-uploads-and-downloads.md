有了对 blob 的引用后, 即可上载和下载数据。 `ICloudBlob`对象具有`Upload`支持`Download`作为源和目标的字节数组、流和文件的方法和方法。 特定类型具有&mdash;更多方便的方法, 例如`CloudBlockBlob` , 支持使用和`UploadTextAsync` `DownloadTextAsync`在上传和下载字符串。

## <a name="creating-new-blobs"></a>创建新的 blob

若要创建新的 blob, 请调用对存储`Upload`中不存在的 blob 的引用的方法之一。 这将执行两项操作: 在存储区中创建 blob 并上载数据。

## <a name="moving-data-to-and-from-blobs"></a>在 blob 之间移动数据

在 blob 之间移动数据是一种需要花费时间的网络操作。 在适用于 .net Core 的 Azure 存储 SDK 中, 所有需要网络活动返回`Task`的方法, 因此请确保正确`await`地在控制器方法中使用。

处理大型数据对象时的一个常见建议是使用流, 而不是内存中的结构, 如字节数组或字符串。 这样可避免在将完整内容发送到目标之前对内存中的内容进行缓冲。 ASP.NET Core 支持从请求和响应读取和写入流。

## <a name="concurrent-access"></a>并发访问

当您的应用程序正在使用时, 其他进程可能会添加、更改或删除 blob。 始终对 defensively 进行编码并考虑由并发导致的问题, 例如, 在您尝试从这些文件中下载时被删除的 blob, 或者在您不希望其内容发生更改的 blob。 有关使用 AccessConditions 和 blob 租用管理并发 blob 访问的信息, 请参阅本模块结尾的其他阅读部分。

## <a name="exercise"></a>健身

让我们通过添加上载和下载代码来完成应用, 然后将其部署到 Azure 应用服务进行测试。

### <a name="upload"></a>[

若要上传 blob, 我们将实现`BlobStorage.Save`使用`GetBlockBlobReference`从容器获取的`CloudBlockBlob`方法。 `FilesController.Upload`将文件流传递给`Save`, 以便我们可以使用`UploadFromStreamAsync`执行上载以实现最大效率。

在编辑器中, 将`Save`替换`BlobStorage.cs`为以下代码:

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
> 此处显示的基于流的上载代码比在将文件发送到 Azure Blob 存储之前将文件读取到字节数组中的效率更高。 但是, 我们用来`IFormFile`从客户端获取文件的 ASP.NET 核心技术并不是真正的端到端流实现, 仅适用于处理小文件的上载。 有关完全流式文件上载的信息, 请参阅本模块结尾的进一步阅读部分。

### <a name="download"></a>下载

`BlobStorage.Load`返回一个`Stream`, 意味着我们的代码不需要实际移动 blob 存储&mdash;中的字节, 只需返回对 blob 流的引用。 可以使用`OpenReadAsync`来执行此操作。 ASP.NET 核心将在生成客户端响应时处理读取和关闭流。

将`Load`替换为此代码并保存您的工作:

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a>在 Azure 中部署和运行

我们的应用程序&mdash;已完成, 让我们对其进行部署, 并查看它能否正常工作。 使用存储帐户连接字符串和容器名称的应用程序设置创建 app Service 应用并对其进行配置。 获取存储帐户的连接字符串`az storage account show-connection-string` , 并将容器的名称设置为。 `files`

应用名称必须是全局唯一的, 因此需要选择自己的`<your-unique-app-name>`名称以进行填写。

```azurecli
az appservice plan create --name blob-exercise-plan --resource-group <rgn>[sandbox resource group name]</rgn>
az webapp create --name <your-unique-app-name> --plan blob-exercise-plan --resource-group <rgn>[sandbox resource group name]</rgn>
CONNECTIONSTRING=$(az storage account show-connection-string --name <your-unique-storage-account-name> --output tsv)
az webapp config appsettings set --name <your-unique-app-name> --resource-group <rgn>[sandbox resource group name]</rgn> --settings AzureStorageConfig:ConnectionString=$CONNECTIONSTRING AzureStorageConfig:FileContainerName=files
```

现在我们将部署应用程序。 下面的命令将网站发布到`pub`文件夹, 将其压缩到`site.zip`, 并将 zip 部署到 App Service。

> [!NOTE]
> 运行以下命令之前, 请确保您`mslearn-store-data-in-azure/store-app-data-with-azure-blob-storage/src/start`的命令行管理程序仍在目录中。

```azurecli
dotnet publish -o pub
cd pub
zip -r ../site.zip *
az webapp deployment source config-zip --src ../site.zip --name <your-unique-app-name> --resource-group <rgn>[sandbox resource group name]</rgn>
```

在`https://<your-unique-app-name>.azurewebsites.net`浏览器中打开以查看正在运行的应用程序。 其外观应如下图所示。

![FileUploader web 应用程序的屏幕截图](../media/7-fileuploader-empty.PNG)

尝试上载并下载一些文件以测试应用程序。 上载一些文件后, 请在命令行管理程序中运行以下命令, 以查看已上载到容器的 blob:

```console
az storage blob list --account-name <your-unique-storage-account-name> --container-name files --query [].{Name:name} --output table
```