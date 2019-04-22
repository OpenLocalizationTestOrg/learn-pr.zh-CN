<span data-ttu-id="56652-101">一旦我们了解如何跨存储帐户、容器和 blob 存储数据, 我们就可以考虑我们需要创建的 Azure 资源来支持应用。</span><span class="sxs-lookup"><span data-stu-id="56652-101">Once we have an idea of how we're going to store data across storage accounts, containers and blobs, we can think about the Azure resources we need to create to support the app.</span></span>

### <a name="storage-accounts"></a><span data-ttu-id="56652-102">存储帐户</span><span class="sxs-lookup"><span data-stu-id="56652-102">Storage accounts</span></span>

<span data-ttu-id="56652-103">存储帐户创建是部署和运行应用之前发生的管理/管理活动。</span><span class="sxs-lookup"><span data-stu-id="56652-103">Storage account creation is an administrative/management activity that takes place prior to deploying and running your app.</span></span> <span data-ttu-id="56652-104">帐户通常由部署或环境安装脚本、Azure 资源管理器模板创建, 或由管理员手动创建。</span><span class="sxs-lookup"><span data-stu-id="56652-104">Accounts are usually created by a deployment or environment setup script, an Azure Resource Manager template, or manually by an administrator.</span></span> <span data-ttu-id="56652-105">除管理工具之外的应用程序通常不应具有创建存储帐户的权限。</span><span class="sxs-lookup"><span data-stu-id="56652-105">Applications other than administrative tools generally should not have permissions to create storage accounts.</span></span>

### <a name="containers"></a><span data-ttu-id="56652-106">存放</span><span class="sxs-lookup"><span data-stu-id="56652-106">Containers</span></span>

<span data-ttu-id="56652-107">与存储帐户创建不同, 创建容器是一个从应用程序中执行的轻型活动。</span><span class="sxs-lookup"><span data-stu-id="56652-107">Unlike storage account creation, container creation is a lightweight activity that makes sense to perform from within an app.</span></span> <span data-ttu-id="56652-108">应用程序在其工作过程中创建和删除容器的情况并不常见。</span><span class="sxs-lookup"><span data-stu-id="56652-108">It's not uncommon for apps to create and delete containers as part of their work.</span></span>

<span data-ttu-id="56652-109">对于依赖于具有硬编码或预配置名称的已知容器集的应用程序, 通常的做法是让应用在启动时创建所需的容器, 如果它们尚不存在, 则使用第一次使用。</span><span class="sxs-lookup"><span data-stu-id="56652-109">For apps that rely on a known set of containers with hard-coded or preconfigured names, typical practice is to let the app create the containers it needs on startup or first usage if they don't already exist.</span></span> <span data-ttu-id="56652-110">如果让您的应用程序创建容器, 而不是将其作为应用程序的部署的一部分, 则无需应用程序和部署过程来了解应用程序使用的容器的名称。</span><span class="sxs-lookup"><span data-stu-id="56652-110">Letting your app create containers instead of doing it as part of your app's deployment eliminates the need for both your application and your deployment process to know the names of the containers the app uses.</span></span>

## <a name="exercise"></a><span data-ttu-id="56652-111">健身</span><span class="sxs-lookup"><span data-stu-id="56652-111">Exercise</span></span>

<span data-ttu-id="56652-112">我们将通过添加代码来使用 Azure Blob 存储来完成未完成的 ASP.NET 核心应用。</span><span class="sxs-lookup"><span data-stu-id="56652-112">We're going to complete an unfinished ASP.NET Core app by adding code to use Azure Blob storage.</span></span> <span data-ttu-id="56652-113">此练习更详细地介绍了如何浏览 Blob 存储 API, 而不仅仅是设计组织和命名方案, 但下面是有关应用程序及其存储数据的方式的快速概述。</span><span class="sxs-lookup"><span data-stu-id="56652-113">This exercise is more about exploring the Blob storage API than it is about designing an organization and naming scheme, but here's a quick overview of the app and how it stores data.</span></span>

![FileUploader web 应用程序的屏幕截图](../media/4-fileuploader-with-files.PNG)

<span data-ttu-id="56652-115">我们的应用程序的工作方式类似于接受文件上载并使其可供下载的共享文件夹。</span><span class="sxs-lookup"><span data-stu-id="56652-115">Our app works like a shared folder that accepts file uploads and makes them available for download.</span></span> <span data-ttu-id="56652-116">它不使用数据库来组织 blob &mdash; , 它会 sanitizes 上载文件的名称, 并直接将其用作 blob 名称。</span><span class="sxs-lookup"><span data-stu-id="56652-116">It doesn't use a database for organizing blobs &mdash; instead, it sanitizes the names of uploaded files and uses them as blob names directly.</span></span> <span data-ttu-id="56652-117">所有上载的文件都存储在单个容器中。</span><span class="sxs-lookup"><span data-stu-id="56652-117">All uploaded files are stored in a single container.</span></span>

<span data-ttu-id="56652-118">我们将首先编译和运行的代码, 但负责存储和加载数据的部分是空的。</span><span class="sxs-lookup"><span data-stu-id="56652-118">The code we'll start with compiles and runs, but the parts responsible for storing and loading data are empty.</span></span> <span data-ttu-id="56652-119">完成此代码后, 我们会将应用程序部署到 Azure 应用服务, 并对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="56652-119">After we complete the code, we'll deploy the app to Azure App Service and test it.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="56652-120">让我们为我们的应用程序设置存储基础结构。</span><span class="sxs-lookup"><span data-stu-id="56652-120">Let's set up the storage infrastructure for our app.</span></span>

### <a name="storage-account"></a><span data-ttu-id="56652-121">存储帐户</span><span class="sxs-lookup"><span data-stu-id="56652-121">Storage account</span></span>

<span data-ttu-id="56652-122">我们将通过 azure CLI 使用 azure 云命令行管理程序创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="56652-122">We'll use the Azure Cloud Shell with the Azure CLI to create a storage account.</span></span> <span data-ttu-id="56652-123">你需要为存储帐户&mdash;提供一个唯一的名称, 以便稍后对其进行记录。</span><span class="sxs-lookup"><span data-stu-id="56652-123">You'll need to provide a unique name for the storage account &mdash; make a note of it for later.</span></span> <span data-ttu-id="56652-124">在下面的示例中, 我们使用的是 "东 US", 但您可以将其更改为 "任何可用的位置" 列表中的。</span><span class="sxs-lookup"><span data-stu-id="56652-124">We're using "East US" in the example below, but you can change it to any of the available locations from list.</span></span>

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="56652-125">执行以下命令以创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="56652-125">Execute the following command to create the storage account.</span></span> 

```azurecli
az storage account create \
  --kind StorageV2 \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --location eastus \
  --name <your-unique-storage-account-name>
```

> [!NOTE]
> <span data-ttu-id="56652-126">为什么`--kind StorageV2`？</span><span class="sxs-lookup"><span data-stu-id="56652-126">Why `--kind StorageV2`?</span></span> <span data-ttu-id="56652-127">有几种不同类型的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="56652-127">There are a few different kinds of storage accounts.</span></span> <span data-ttu-id="56652-128">在大多数情况下, 应使用通用 v2 帐户。</span><span class="sxs-lookup"><span data-stu-id="56652-128">For most scenarios, you should use general-purpose v2 accounts.</span></span> <span data-ttu-id="56652-129">您需要明确指定`--kind StorageV2`的唯一原因是, 通用 v2 帐户仍是非常新的, 并且尚未在 azure 门户或 azure CLI 中进行默认设置。</span><span class="sxs-lookup"><span data-stu-id="56652-129">The only reason you need to explicitly specify `--kind StorageV2` is that general-purpose v2 accounts are still fairly new and have not yet been made the default in the Azure Portal or the Azure CLI.</span></span>

### <a name="container"></a><span data-ttu-id="56652-130">Container</span><span class="sxs-lookup"><span data-stu-id="56652-130">Container</span></span>

<span data-ttu-id="56652-131">我们将在此模块中使用的应用程序使用单个容器。</span><span class="sxs-lookup"><span data-stu-id="56652-131">The app we'll be working with in this module uses a single container.</span></span> <span data-ttu-id="56652-132">我们将按照最佳做法, 让应用在启动时创建容器。</span><span class="sxs-lookup"><span data-stu-id="56652-132">We're going to follow the best practice of letting the app create the container at startup.</span></span> <span data-ttu-id="56652-133">但是, 可以从 Azure CLI 中执行容器创建: 如果想`az storage container create -h`要查看文档, 请在云命令行管理程序终端中运行。</span><span class="sxs-lookup"><span data-stu-id="56652-133">However, container creation can be done from the Azure CLI: run `az storage container create -h` in the Cloud Shell terminal if you'd like to see the documentation.</span></span>