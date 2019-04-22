<span data-ttu-id="f7e45-101">以下是使用 Azure Blob 存储的应用程序的典型工作流:</span><span class="sxs-lookup"><span data-stu-id="f7e45-101">The following is the typical workflow for apps that use Azure Blob storage:</span></span>

1. <span data-ttu-id="f7e45-102">**检索配置**: 启动时加载存储帐户配置。</span><span class="sxs-lookup"><span data-stu-id="f7e45-102">**Retrieve configuration**: At startup, load the storage account configuration.</span></span> <span data-ttu-id="f7e45-103">这通常是一个存储帐户连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f7e45-103">This is typically a storage account connection string.</span></span>

1. <span data-ttu-id="f7e45-104">**初始化客户端**: 使用连接字符串初始化 Azure 存储客户端库。</span><span class="sxs-lookup"><span data-stu-id="f7e45-104">**Initialize client**: Use the connection string to initialize the Azure Storage client library.</span></span> <span data-ttu-id="f7e45-105">这将创建应用程序将用来处理 Blob 存储 API 的对象。</span><span class="sxs-lookup"><span data-stu-id="f7e45-105">This creates the objects the app will use to work with the Blob storage API.</span></span>

1. <span data-ttu-id="f7e45-106">**使用**: 使用客户端库进行 API 调用, 以在容器和 blob 上运行。</span><span class="sxs-lookup"><span data-stu-id="f7e45-106">**Use**: Make API calls with the client library to operate on containers and blobs.</span></span>

## <a name="configure-your-connection-string"></a><span data-ttu-id="f7e45-107">配置连接字符串</span><span class="sxs-lookup"><span data-stu-id="f7e45-107">Configure your connection string</span></span>

<span data-ttu-id="f7e45-108">在运行您的应用程序之前, 你将需要使用的存储帐户的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f7e45-108">Before running your app, you'll need the connection string for the storage account you will use.</span></span> <span data-ttu-id="f7e45-109">您可以使用任何 azure 管理接口来获取它, 包括 azure 门户、azure CLI 或 azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f7e45-109">You can use any Azure management interface to get it, including the Azure portal, the Azure CLI or Azure PowerShell.</span></span> <span data-ttu-id="f7e45-110">当我们将 web 应用程序设置为在本模块结尾附近运行代码时, 我们将使用 Azure CLI 获取之前创建的存储帐户的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f7e45-110">When we set up the web app to run our code near the end of this module, we'll use the Azure CLI to get the connection string for the storage account you created earlier.</span></span>

<span data-ttu-id="f7e45-111">存储帐户连接字符串包含帐户密钥。</span><span class="sxs-lookup"><span data-stu-id="f7e45-111">Storage account connection strings include the account key.</span></span> <span data-ttu-id="f7e45-112">帐户密钥被视为秘密, 应安全地存储。</span><span class="sxs-lookup"><span data-stu-id="f7e45-112">The account key is considered a secret and should be stored securely.</span></span> <span data-ttu-id="f7e45-113">在这里, 我们将把连接字符串存储在应用服务应用程序设置中。</span><span class="sxs-lookup"><span data-stu-id="f7e45-113">Here, we will store the connection string in an App Service application setting.</span></span> <span data-ttu-id="f7e45-114">App Service 应用程序设置是应用程序机密的安全位置, 但此设计不支持本地开发, 也不是其自己的强大端到端解决方案。</span><span class="sxs-lookup"><span data-stu-id="f7e45-114">App Service application settings are a secure place for application secrets, but this design does not support local development and is not a robust, end-to-end solution on its own.</span></span>

> [!WARNING]
> <span data-ttu-id="f7e45-115">**不要将存储帐户密钥放在代码中或未受保护的配置文件中。**</span><span class="sxs-lookup"><span data-stu-id="f7e45-115">**Do not place storage account keys in code or in unprotected configuration files.**</span></span> <span data-ttu-id="f7e45-116">存储帐户密钥可实现对存储帐户的完全访问权限。</span><span class="sxs-lookup"><span data-stu-id="f7e45-116">Storage account keys enable full access to your storage account.</span></span> <span data-ttu-id="f7e45-117">泄漏密钥可能导致无法恢复的损坏和大型帐单。</span><span class="sxs-lookup"><span data-stu-id="f7e45-117">Leaking a key can result in unrecoverable damage and large bills.</span></span> <span data-ttu-id="f7e45-118">请参阅本模块末尾的进一步阅读部分, 了解有关如何从泄露密钥中恢复的存储指南和建议。</span><span class="sxs-lookup"><span data-stu-id="f7e45-118">See the Further Reading section at the end of this module for storage guidance and advice about how to recover from a leaked key.</span></span>

## <a name="initialize-the-blob-storage-object-model"></a><span data-ttu-id="f7e45-119">初始化 Blob 存储对象模型</span><span class="sxs-lookup"><span data-stu-id="f7e45-119">Initialize the Blob storage object model</span></span>

<span data-ttu-id="f7e45-120">在适用于 .net Core 的 Azure 存储 SDK 中, 使用 Blob 存储的标准模式包含以下步骤:</span><span class="sxs-lookup"><span data-stu-id="f7e45-120">In the Azure Storage SDK for .NET Core, the standard pattern for using Blob storage consists of the following steps:</span></span>

1. <span data-ttu-id="f7e45-121">使用`CloudStorageAccount.Parse`连接字符串`TryParse`调用 (或) 以获取`CloudStorageAccount`。</span><span class="sxs-lookup"><span data-stu-id="f7e45-121">Call `CloudStorageAccount.Parse` (or `TryParse`) with your connection string to get a `CloudStorageAccount`.</span></span>

1. <span data-ttu-id="f7e45-122">上`CreateCloudBlobClient`的`CloudStorageAccount`调用来获取`CloudBlobClient`。</span><span class="sxs-lookup"><span data-stu-id="f7e45-122">Call `CreateCloudBlobClient` on the `CloudStorageAccount` to get a `CloudBlobClient`.</span></span>

1. <span data-ttu-id="f7e45-123">上`GetContainerReference`的`CloudBlobClient`调用来获取`CloudBlobContainer`。</span><span class="sxs-lookup"><span data-stu-id="f7e45-123">Call `GetContainerReference` on the `CloudBlobClient` to get a `CloudBlobContainer`.</span></span>

1. <span data-ttu-id="f7e45-124">使用容器上的方法获取 blob 列表和/或获取对各个 blob 的引用, 以上载和下载数据。</span><span class="sxs-lookup"><span data-stu-id="f7e45-124">Use methods on the container to get a list of blobs and/or get references to individual blobs to upload and download data.</span></span>

<span data-ttu-id="f7e45-125">在代码中, 步骤&ndash;1 3 如下所示:</span><span class="sxs-lookup"><span data-stu-id="f7e45-125">In code, steps 1&ndash;3 look like this:</span></span>

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

<span data-ttu-id="f7e45-126">此初始化代码中的任何一个都不会通过网络进行调用。</span><span class="sxs-lookup"><span data-stu-id="f7e45-126">None of this initialization code makes calls over the network.</span></span> <span data-ttu-id="f7e45-127">这意味着, 由于不正确的信息而发生的一些异常将不会在以后引发。</span><span class="sxs-lookup"><span data-stu-id="f7e45-127">This means that some exceptions that occur because of incorrect information won't be thrown until later.</span></span> <span data-ttu-id="f7e45-128">例如, 如果连接字符串格式`CloudStorageAccount.Parse`不正确, 则调用将立即引发异常, 但如果连接字符串指向的存储帐户不存在, 则不会引发异常。</span><span class="sxs-lookup"><span data-stu-id="f7e45-128">For example, the call to `CloudStorageAccount.Parse` will throw an exception immediately if the connection string is formatted incorrectly, but no exception will be thrown if the storage account that a connection string points to doesn't exist.</span></span>

## <a name="create-containers-at-startup"></a><span data-ttu-id="f7e45-129">启动时创建容器</span><span class="sxs-lookup"><span data-stu-id="f7e45-129">Create containers at startup</span></span>

<span data-ttu-id="f7e45-130">调用`CreateIfNotExistsAsync` a `CloudBlobContainer`是在应用程序启动或首次尝试使用时创建容器的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="f7e45-130">Calling `CreateIfNotExistsAsync` on a `CloudBlobContainer` is the best way to create a container when your application starts or when it first tries to use it.</span></span>

<span data-ttu-id="f7e45-131">`CreateIfNotExistsAsync`如果容器已存在, 则不会引发异常, 但会对 Azure 存储进行网络调用。</span><span class="sxs-lookup"><span data-stu-id="f7e45-131">`CreateIfNotExistsAsync` won't throw an exception if the container already exists, but it does make a network call to Azure Storage.</span></span> <span data-ttu-id="f7e45-132">在初始化期间调用一次, 而不是每次尝试使用容器时调用。</span><span class="sxs-lookup"><span data-stu-id="f7e45-132">Call it once during initialization, not every time you try to use a container.</span></span>

## <a name="exercise"></a><span data-ttu-id="f7e45-133">健身</span><span class="sxs-lookup"><span data-stu-id="f7e45-133">Exercise</span></span>

### <a name="clone-and-explore-the-unfinished-app"></a><span data-ttu-id="f7e45-134">克隆并浏览未完成的应用程序</span><span class="sxs-lookup"><span data-stu-id="f7e45-134">Clone and explore the unfinished app</span></span>

<span data-ttu-id="f7e45-135">首先, 让我们从 GitHub 克隆初学者应用。</span><span class="sxs-lookup"><span data-stu-id="f7e45-135">First, let's clone the starter app from GitHub.</span></span> <span data-ttu-id="f7e45-136">在云命令行管理程序终端中, 运行以下命令以获取源代码的副本并在编辑器中打开它:</span><span class="sxs-lookup"><span data-stu-id="f7e45-136">In the Cloud Shell terminal, run the following command to get a copy of the source code and open it in the editor:</span></span>

```console
git clone https://github.com/MicrosoftDocs/mslearn-store-data-in-azure.git
cd mslearn-store-data-in-azure/store-app-data-with-azure-blob-storage/src/start
code .
```

<span data-ttu-id="f7e45-137">在编辑器中`Controllers/FilesController.cs`打开该文件。</span><span class="sxs-lookup"><span data-stu-id="f7e45-137">Open the file `Controllers/FilesController.cs` in the editor.</span></span> <span data-ttu-id="f7e45-138">此处没有可执行的操作, 但我们将快速了解应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="f7e45-138">There's no work to do here, but we're going to have a quick look at what the app does.</span></span>

<span data-ttu-id="f7e45-139">此控制器实现具有三个操作的 API:</span><span class="sxs-lookup"><span data-stu-id="f7e45-139">This controller implements an API with three actions:</span></span>

- <span data-ttu-id="f7e45-140">**索引**(GET/api/Files) 返回一个 url 列表, 每个 url 对应一个上载的文件。</span><span class="sxs-lookup"><span data-stu-id="f7e45-140">**Index** (GET /api/Files) returns a list of URLs, one for each file that's been uploaded.</span></span> <span data-ttu-id="f7e45-141">应用程序前端调用此方法, 以生成指向已上载文件的超链接列表。</span><span class="sxs-lookup"><span data-stu-id="f7e45-141">The app front end calls this method to build a list of hyperlinks to the uploaded files.</span></span>
- <span data-ttu-id="f7e45-142">**上传**(POST/api/Files) 接收上载的文件并将其保存。</span><span class="sxs-lookup"><span data-stu-id="f7e45-142">**Upload** (POST /api/Files) receives an uploaded file and saves it.</span></span>
- <span data-ttu-id="f7e45-143">**下载**(GET/api/Files/{filename}) 按其名称下载单个文件。</span><span class="sxs-lookup"><span data-stu-id="f7e45-143">**Download** (GET /api/Files/{filename}) downloads an individual file by its name.</span></span>

<span data-ttu-id="f7e45-144">每个方法都`IStorage`使用一个`storage`调用的实例来完成其工作。</span><span class="sxs-lookup"><span data-stu-id="f7e45-144">Each method uses an `IStorage` instance called `storage` to do its work.</span></span> <span data-ttu-id="f7e45-145">中`Models/BlobStorage.cs`有一个不完整的`IStorage`实现, 我们打算填写。</span><span class="sxs-lookup"><span data-stu-id="f7e45-145">There is an incomplete implementation of `IStorage` in `Models/BlobStorage.cs` that we're going to fill in.</span></span>

### <a name="add-the-nuget-package"></a><span data-ttu-id="f7e45-146">添加 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="f7e45-146">Add the NuGet package</span></span>

<span data-ttu-id="f7e45-147">首先, 添加对 Azure 存储 SDK 的引用。</span><span class="sxs-lookup"><span data-stu-id="f7e45-147">First, add a reference to the Azure Storage SDK.</span></span> <span data-ttu-id="f7e45-148">在终端中, 运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="f7e45-148">In the terminal, run the following:</span></span>

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

<span data-ttu-id="f7e45-149">这将确保我们使用的是最新版本的 Blob 存储客户端库。</span><span class="sxs-lookup"><span data-stu-id="f7e45-149">This will make sure we're using the newest version of the Blob storage client library.</span></span>

### <a name="configure"></a><span data-ttu-id="f7e45-150">对</span><span class="sxs-lookup"><span data-stu-id="f7e45-150">Configure</span></span>

<span data-ttu-id="f7e45-151">我们需要的配置值是存储帐户连接字符串和应用程序将用来存储文件的容器的名称。</span><span class="sxs-lookup"><span data-stu-id="f7e45-151">The configuration values we need are the storage account connection string and the name of the container the app will use to store files.</span></span> <span data-ttu-id="f7e45-152">在本模块中, 我们只打算在 Azure 应用服务中运行应用程序, 因此我们将遵循应用服务最佳实践并将值存储在 app service 应用程序设置中。</span><span class="sxs-lookup"><span data-stu-id="f7e45-152">In this module, we're only going to run the app in Azure App Service, so we'll follow App Service best practice and store the values in App Service application settings.</span></span> <span data-ttu-id="f7e45-153">我们将在创建应用服务实例时执行此操作, 因此我们现在不需要执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="f7e45-153">We'll do that when we create the App Service instance, so there's nothing we need to do at the moment.</span></span>

<span data-ttu-id="f7e45-154">在*使用*配置时, 我们的初学者应用程序已经包含我们需要的管道。</span><span class="sxs-lookup"><span data-stu-id="f7e45-154">When it comes to *using* the configuration, our starter app already includes the plumbing we need.</span></span> <span data-ttu-id="f7e45-155">中`IOptions<AzureStorageConfig>` `BlobStorage`的构造函数参数具有两个属性: 存储帐户连接字符串和容器的名称, 我们的应用程序将在其中存储 blob。</span><span class="sxs-lookup"><span data-stu-id="f7e45-155">The `IOptions<AzureStorageConfig>` constructor parameter in `BlobStorage` has two properties: the storage account connection string and the name of the container our app will store blobs in.</span></span> <span data-ttu-id="f7e45-156">中的`ConfigureServices`方法中存在`Startup.cs`的代码在应用程序启动时加载配置值。</span><span class="sxs-lookup"><span data-stu-id="f7e45-156">There is code in the `ConfigureServices` method of `Startup.cs` that loads the values from configuration when the app starts.</span></span>

### <a name="initialize"></a><span data-ttu-id="f7e45-157">格式化</span><span class="sxs-lookup"><span data-stu-id="f7e45-157">Initialize</span></span>

<span data-ttu-id="f7e45-158">在`Models/BlobStorage.cs`编辑器中打开。</span><span class="sxs-lookup"><span data-stu-id="f7e45-158">Open `Models/BlobStorage.cs` in the editor.</span></span> <span data-ttu-id="f7e45-159">将以下`using`语句添加到文件顶部, 以便为要在练习中添加的代码准备它。</span><span class="sxs-lookup"><span data-stu-id="f7e45-159">Add the following `using` statements to the top of the file to prepare it for the code you're going to add during the exercise.</span></span>

```csharp
using System.Linq;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="f7e45-160">查找`Initialize`方法。</span><span class="sxs-lookup"><span data-stu-id="f7e45-160">Locate the `Initialize` method.</span></span> <span data-ttu-id="f7e45-161">在首次使用时`BlobStorage` , 我们的应用程序将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="f7e45-161">Our app will call this method when `BlobStorage` is used for the first time.</span></span> <span data-ttu-id="f7e45-162">如果您感到好奇, 可以查看`ConfigureServices`中的`Startup.cs`以了解如何完成此操作。</span><span class="sxs-lookup"><span data-stu-id="f7e45-162">If you're curious, you can look at `ConfigureServices` in `Startup.cs` to see how this is done.</span></span>

<span data-ttu-id="f7e45-163">`Initialize`是我们想要创建容器 (如果它尚不存在) 的位置。</span><span class="sxs-lookup"><span data-stu-id="f7e45-163">`Initialize` is where we want to create our container if it doesn't already exist.</span></span> <span data-ttu-id="f7e45-164">将当前的实现替换`Initialize`为以下代码并保存您的工作:</span><span class="sxs-lookup"><span data-stu-id="f7e45-164">Replace the current implementation of `Initialize` with the following code and save your work:</span></span>

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```