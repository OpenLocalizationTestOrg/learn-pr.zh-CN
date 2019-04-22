<span data-ttu-id="773d5-101">Azure CLI 允许您键入命令, 并立即从命令行执行这些命令。</span><span class="sxs-lookup"><span data-stu-id="773d5-101">The Azure CLI lets you type commands and execute them immediately from the command line.</span></span> <span data-ttu-id="773d5-102">请记住, 软件开发示例中的总体目标是部署 web 应用程序的新内部版本以供测试。</span><span class="sxs-lookup"><span data-stu-id="773d5-102">Recall that the overall goal in the software development example is to deploy new builds of a web app for testing.</span></span> <span data-ttu-id="773d5-103">我们来讨论您可以使用 Azure CLI 执行的任务的种类。</span><span class="sxs-lookup"><span data-stu-id="773d5-103">Let's talk about the sorts of tasks you can do with the Azure CLI.</span></span>

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a><span data-ttu-id="773d5-104">哪些 azure 资源可以使用 azure CLI 进行管理？</span><span class="sxs-lookup"><span data-stu-id="773d5-104">What Azure resources can be managed using the Azure CLI?</span></span>

<span data-ttu-id="773d5-105">通过 azure CLI, 你可以控制每个 Azure 资源的几乎每个方面。</span><span class="sxs-lookup"><span data-stu-id="773d5-105">The Azure CLI lets you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="773d5-106">您可以使用资源组、存储、虚拟机、azure Active Directory (azure AD)、容器、机器学习等。</span><span class="sxs-lookup"><span data-stu-id="773d5-106">You can work with resource groups, storage, virtual machines, Azure Active Directory (Azure AD), containers, machine learning, and so on.</span></span>

<span data-ttu-id="773d5-107">CLI 中的命令是按_组_和_子_组进行构造的。</span><span class="sxs-lookup"><span data-stu-id="773d5-107">Commands in the CLI are structured in _groups_ and _subgroups_.</span></span> <span data-ttu-id="773d5-108">每个组代表一个由 Azure 提供的服务, 子组将这些服务的命令分成一个逻辑分组。</span><span class="sxs-lookup"><span data-stu-id="773d5-108">Each group represents a service provided by Azure, and the subgroups divide commands for these services into logical groupings.</span></span> <span data-ttu-id="773d5-109">`storage`例如, 组包含子组, 其中**包括帐户**、 **blob**、**存储**和**队列**。</span><span class="sxs-lookup"><span data-stu-id="773d5-109">For example, the `storage` group contains subgroups including **account**, **blob**, **storage**, and **queue**.</span></span>

<span data-ttu-id="773d5-110">那么, 您如何查找所需的特定命令呢？</span><span class="sxs-lookup"><span data-stu-id="773d5-110">So, how do you find the particular commands you need?</span></span> <span data-ttu-id="773d5-111">一种方法是使用`az find`。</span><span class="sxs-lookup"><span data-stu-id="773d5-111">One way is to use `az find`.</span></span> <span data-ttu-id="773d5-112">例如, 如果您要查找可能有助于管理存储 blob 的命令, 则可以使用以下 find 命令:</span><span class="sxs-lookup"><span data-stu-id="773d5-112">For example, if you want to find commands that might help you manage a storage blob, you can use the following find command:</span></span>

```azurecli
az find -q blob
```

<span data-ttu-id="773d5-113">如果您已经知道所需的命令的名称, 则该`--help`命令的参数将提供有关命令的更多详细信息, 以及命令组的可用子命令的列表。</span><span class="sxs-lookup"><span data-stu-id="773d5-113">If you already know the name of the command you want, the `--help` argument for that command will get you more detailed information on the command, and for a command group, a list of the available subcommands.</span></span> <span data-ttu-id="773d5-114">因此, 在我们的存储示例中, 您可以通过以下方式获取子组的列表和用于管理 blob 存储的命令:</span><span class="sxs-lookup"><span data-stu-id="773d5-114">So, with our storage example, here's how you can get a list of the subgroups and commands for managing blob storage:</span></span>

```azurecli
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a><span data-ttu-id="773d5-115">如何创建 Azure 资源</span><span class="sxs-lookup"><span data-stu-id="773d5-115">How to create an Azure resource</span></span>

<span data-ttu-id="773d5-116">创建新的 Azure 资源时, 通常有三个步骤: 连接到 Azure 订阅, 创建资源, 并验证创建是否成功。</span><span class="sxs-lookup"><span data-stu-id="773d5-116">When creating a new Azure resource, there are typically three steps: connect to your Azure subscription, create the resource, and verify that creation was successful.</span></span> <span data-ttu-id="773d5-117">下图显示了该过程的高级概述。</span><span class="sxs-lookup"><span data-stu-id="773d5-117">The following illustration shows a high-level overview of the process.</span></span>

![该图显示了使用命令行界面创建 Azure 资源的步骤。](../media/4-create-resources-overview.png)

<span data-ttu-id="773d5-119">每个步骤对应于不同的 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="773d5-119">Each step corresponds to a different Azure CLI command.</span></span>

### <a name="connect"></a><span data-ttu-id="773d5-120">连接</span><span class="sxs-lookup"><span data-stu-id="773d5-120">Connect</span></span>

<span data-ttu-id="773d5-121">由于你使用的是 azure cli 的本地安装, 因此需要先进行身份验证, 然后才能执行 azure 命令, 方法是使用 azure cli**登录**命令。</span><span class="sxs-lookup"><span data-stu-id="773d5-121">Since you're working with a local install of the Azure CLI, you'll need to authenticate before you can execute Azure commands, by using the Azure CLI **login** command.</span></span>

```azurecli
az login
```

<span data-ttu-id="773d5-122">azure CLI 通常会启动您的默认浏览器, 以打开 Azure 登录页。</span><span class="sxs-lookup"><span data-stu-id="773d5-122">The Azure CLI will typically launch your default browser to open the Azure sign-in page.</span></span> <span data-ttu-id="773d5-123">如果这样做不起作用, 请按照命令行说明操作, 并在[https://aka.ms/devicelogin](https://aka.ms/devicelogin)中输入授权代码。</span><span class="sxs-lookup"><span data-stu-id="773d5-123">If this doesn't work, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

<span data-ttu-id="773d5-124">登录成功后, 你将连接到你的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="773d5-124">After a successful sign in, you'll be connected to your Azure subscription.</span></span>

### <a name="create"></a><span data-ttu-id="773d5-125">Create</span><span class="sxs-lookup"><span data-stu-id="773d5-125">Create</span></span>

<span data-ttu-id="773d5-126">您通常需要在创建新的 Azure 服务之前创建新的资源组, 因此我们将使用资源组作为示例来说明如何从 CLI 创建 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="773d5-126">You'll often need to create a new resource group before you create a new Azure service, so we'll use resource groups as an example to show how to create Azure resources from the CLI.</span></span>

<span data-ttu-id="773d5-127">Azure CLI**组 create**命令创建一个资源组。</span><span class="sxs-lookup"><span data-stu-id="773d5-127">The Azure CLI **group create** command creates a resource group.</span></span> <span data-ttu-id="773d5-128">您必须指定名称和位置。</span><span class="sxs-lookup"><span data-stu-id="773d5-128">You must specify a name and location.</span></span> <span data-ttu-id="773d5-129">该名称在你的订阅中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="773d5-129">The name must be unique within your subscription.</span></span> <span data-ttu-id="773d5-130">该位置确定将存储资源组的元数据的位置。</span><span class="sxs-lookup"><span data-stu-id="773d5-130">The location determines where the metadata for your resource group will be stored.</span></span> <span data-ttu-id="773d5-131">您可以使用如 "west US"、"北欧" 或 "西印度" 指定位置的字符串;或者, 可以使用单个等效词, 如 westus、northeurope 或 westindia。</span><span class="sxs-lookup"><span data-stu-id="773d5-131">You use strings like "West US", "North Europe", or "West India" to specify the location; alternatively, you can use single word equivalents, such as westus, northeurope, or westindia.</span></span> <span data-ttu-id="773d5-132">核心语法为:</span><span class="sxs-lookup"><span data-stu-id="773d5-132">The core syntax is:</span></span>

```azurecli
az group create --name <name> --location <location>
```

> [!IMPORTANT]
> <span data-ttu-id="773d5-133">使用免费的 Azure 沙箱时, 不需要创建资源组。</span><span class="sxs-lookup"><span data-stu-id="773d5-133">You do not need to create a resource group when using the free Azure sandbox.</span></span> <span data-ttu-id="773d5-134">相反, 您将使用预先创建的资源组。</span><span class="sxs-lookup"><span data-stu-id="773d5-134">Instead, you will use a pre-created resource group.</span></span>

### <a name="verify"></a><span data-ttu-id="773d5-135">Verify</span><span class="sxs-lookup"><span data-stu-id="773d5-135">Verify</span></span>

<span data-ttu-id="773d5-136">对于许多 azure 资源, azure CLI 提供了用于查看资源详细信息的**列表**子命令。</span><span class="sxs-lookup"><span data-stu-id="773d5-136">For many Azure resources, the Azure CLI provides a **list** subcommand to view resource details.</span></span> <span data-ttu-id="773d5-137">例如, azure CLI**组列表**命令列出了 azure 资源组。</span><span class="sxs-lookup"><span data-stu-id="773d5-137">For example, the Azure CLI **group list** command lists your Azure resource groups.</span></span> <span data-ttu-id="773d5-138">在这里, 可以通过以下方法来验证资源组的创建是否成功:</span><span class="sxs-lookup"><span data-stu-id="773d5-138">This is useful here to verify whether creation of the resource group was successful:</span></span>

```azurecli
az group list
```

<span data-ttu-id="773d5-139">若要获得更简洁的视图, 可以将输出格式设置为简单表格:</span><span class="sxs-lookup"><span data-stu-id="773d5-139">To get a more concise view, you can format the output as a simple table:</span></span>

```azurecli
az group list --output table
```
