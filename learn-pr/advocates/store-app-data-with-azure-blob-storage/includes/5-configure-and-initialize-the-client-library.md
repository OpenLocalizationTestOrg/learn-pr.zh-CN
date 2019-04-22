以下是使用 Azure Blob 存储的应用程序的典型工作流:

1. **检索配置**: 启动时加载存储帐户配置。 这通常是一个存储帐户连接字符串。

1. **初始化客户端**: 使用连接字符串初始化 Azure 存储客户端库。 这将创建应用程序将用来处理 Blob 存储 API 的对象。

1. **使用**: 使用客户端库进行 API 调用, 以在容器和 blob 上运行。

## <a name="configure-your-connection-string"></a>配置连接字符串

在运行您的应用程序之前, 你将需要使用的存储帐户的连接字符串。 您可以使用任何 azure 管理接口来获取它, 包括 azure 门户、azure CLI 或 azure PowerShell。 当我们将 web 应用程序设置为在本模块结尾附近运行代码时, 我们将使用 Azure CLI 获取之前创建的存储帐户的连接字符串。

存储帐户连接字符串包含帐户密钥。 帐户密钥被视为秘密, 应安全地存储。 在这里, 我们将把连接字符串存储在应用服务应用程序设置中。 App Service 应用程序设置是应用程序机密的安全位置, 但此设计不支持本地开发, 也不是其自己的强大端到端解决方案。

> [!WARNING]
> **不要将存储帐户密钥放在代码中或未受保护的配置文件中。** 存储帐户密钥可实现对存储帐户的完全访问权限。 泄漏密钥可能导致无法恢复的损坏和大型帐单。 请参阅本模块末尾的进一步阅读部分, 了解有关如何从泄露密钥中恢复的存储指南和建议。

## <a name="initialize-the-blob-storage-object-model"></a>初始化 Blob 存储对象模型

在适用于 .net Core 的 Azure 存储 SDK 中, 使用 Blob 存储的标准模式包含以下步骤:

1. 使用`CloudStorageAccount.Parse`连接字符串`TryParse`调用 (或) 以获取`CloudStorageAccount`。

1. 上`CreateCloudBlobClient`的`CloudStorageAccount`调用来获取`CloudBlobClient`。

1. 上`GetContainerReference`的`CloudBlobClient`调用来获取`CloudBlobContainer`。

1. 使用容器上的方法获取 blob 列表和/或获取对各个 blob 的引用, 以上载和下载数据。

在代码中, 步骤&ndash;1 3 如下所示:

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

此初始化代码中的任何一个都不会通过网络进行调用。 这意味着, 由于不正确的信息而发生的一些异常将不会在以后引发。 例如, 如果连接字符串格式`CloudStorageAccount.Parse`不正确, 则调用将立即引发异常, 但如果连接字符串指向的存储帐户不存在, 则不会引发异常。

## <a name="create-containers-at-startup"></a>启动时创建容器

调用`CreateIfNotExistsAsync` a `CloudBlobContainer`是在应用程序启动或首次尝试使用时创建容器的最佳方式。

`CreateIfNotExistsAsync`如果容器已存在, 则不会引发异常, 但会对 Azure 存储进行网络调用。 在初始化期间调用一次, 而不是每次尝试使用容器时调用。

## <a name="exercise"></a>健身

### <a name="clone-and-explore-the-unfinished-app"></a>克隆并浏览未完成的应用程序

首先, 让我们从 GitHub 克隆初学者应用。 在云命令行管理程序终端中, 运行以下命令以获取源代码的副本并在编辑器中打开它:

```console
git clone https://github.com/MicrosoftDocs/mslearn-store-data-in-azure.git
cd mslearn-store-data-in-azure/store-app-data-with-azure-blob-storage/src/start
code .
```

在编辑器中`Controllers/FilesController.cs`打开该文件。 此处没有可执行的操作, 但我们将快速了解应用程序的功能。

此控制器实现具有三个操作的 API:

- **索引**(GET/api/Files) 返回一个 url 列表, 每个 url 对应一个上载的文件。 应用程序前端调用此方法, 以生成指向已上载文件的超链接列表。
- **上传**(POST/api/Files) 接收上载的文件并将其保存。
- **下载**(GET/api/Files/{filename}) 按其名称下载单个文件。

每个方法都`IStorage`使用一个`storage`调用的实例来完成其工作。 中`Models/BlobStorage.cs`有一个不完整的`IStorage`实现, 我们打算填写。

### <a name="add-the-nuget-package"></a>添加 NuGet 包

首先, 添加对 Azure 存储 SDK 的引用。 在终端中, 运行以下命令:

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

这将确保我们使用的是最新版本的 Blob 存储客户端库。

### <a name="configure"></a>对

我们需要的配置值是存储帐户连接字符串和应用程序将用来存储文件的容器的名称。 在本模块中, 我们只打算在 Azure 应用服务中运行应用程序, 因此我们将遵循应用服务最佳实践并将值存储在 app service 应用程序设置中。 我们将在创建应用服务实例时执行此操作, 因此我们现在不需要执行任何操作。

在*使用*配置时, 我们的初学者应用程序已经包含我们需要的管道。 中`IOptions<AzureStorageConfig>` `BlobStorage`的构造函数参数具有两个属性: 存储帐户连接字符串和容器的名称, 我们的应用程序将在其中存储 blob。 中的`ConfigureServices`方法中存在`Startup.cs`的代码在应用程序启动时加载配置值。

### <a name="initialize"></a>格式化

在`Models/BlobStorage.cs`编辑器中打开。 将以下`using`语句添加到文件顶部, 以便为要在练习中添加的代码准备它。

```csharp
using System.Linq;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

查找`Initialize`方法。 在首次使用时`BlobStorage` , 我们的应用程序将调用此方法。 如果您感到好奇, 可以查看`ConfigureServices`中的`Startup.cs`以了解如何完成此操作。

`Initialize`是我们想要创建容器 (如果它尚不存在) 的位置。 将当前的实现替换`Initialize`为以下代码并保存您的工作:

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```