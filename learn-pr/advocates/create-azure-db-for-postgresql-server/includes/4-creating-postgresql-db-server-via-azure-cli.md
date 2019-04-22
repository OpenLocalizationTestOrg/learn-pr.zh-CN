<span data-ttu-id="09429-101">此单元将在您实际执行练习以创建服务器时熟悉下一个单元中所执行的步骤。</span><span class="sxs-lookup"><span data-stu-id="09429-101">This unit serves to familiarize you with the steps you'll take in the next unit when you actually perform the exercise to create a server.</span></span> <span data-ttu-id="09429-102">如果你在下一个设备中停滞, 请返回此部分。</span><span class="sxs-lookup"><span data-stu-id="09429-102">Refer back to this section if you get stuck in the next unit.</span></span>

## <a name="scenario"></a><span data-ttu-id="09429-103">方案</span><span class="sxs-lookup"><span data-stu-id="09429-103">Scenario</span></span>

<span data-ttu-id="09429-104">假设你使用的是本地 PostgreSQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="09429-104">Let's assume you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="09429-105">你的公司现在正在寻找通过将你的服务器迁移到 Azure 中而扩展设备支持、可用性、数据跟踪和处理功能的信息。</span><span class="sxs-lookup"><span data-stu-id="09429-105">Your company is now looking at expanding device support, availability, data tracking, and processing features by moving your server into Azure.</span></span> <span data-ttu-id="09429-106">您将研究自动为 PostgreSQL 服务器创建 Azure 数据库所需的工作量。</span><span class="sxs-lookup"><span data-stu-id="09429-106">You'll investigate how much effort it takes to automate the creation of an Azure Database for PostgreSQL server.</span></span>

<span data-ttu-id="09429-107">使用 azure 门户为 PostgreSQL 服务器创建单个 Azure 数据库非常简单。</span><span class="sxs-lookup"><span data-stu-id="09429-107">Creating a single Azure Database for PostgreSQL server using the Azure portal is easy.</span></span> <span data-ttu-id="09429-108">创建多个数据库并在仅使用该门户的情况运行进行中维护可能会变得单调乏味。</span><span class="sxs-lookup"><span data-stu-id="09429-108">Creating more than one database and running on-going maintenance using only the portal may become tedious.</span></span> <span data-ttu-id="09429-109">当您希望自动执行管理任务时, 您将使用 Azure CLI 创建脚本。</span><span class="sxs-lookup"><span data-stu-id="09429-109">You'll use the Azure CLI to create scripts when you want to automate management tasks.</span></span>

<span data-ttu-id="09429-110">使用 azure CLI, 可以自动创建 Microsoft Azure 内几乎所有资源。</span><span class="sxs-lookup"><span data-stu-id="09429-110">Creating almost any resource within Microsoft Azure can be automated using the Azure CLI.</span></span> <span data-ttu-id="09429-111">在此单元中, 你将了解如何使用 azure CLI 自动管理对 PostgreSQL 服务器的 Azure 数据库。</span><span class="sxs-lookup"><span data-stu-id="09429-111">In this unit, you'll learn how to automate management of your Azure Database for PostgreSQL servers using the Azure CLI.</span></span>

## <a name="what-is-the-azure-cli"></a><span data-ttu-id="09429-112">什么是 Azure CLI？</span><span class="sxs-lookup"><span data-stu-id="09429-112">What is the Azure CLI?</span></span>

<span data-ttu-id="09429-113">[azure CLI](https://docs.microsoft.com/cli/azure?azure-portal=true)是 Microsoft 的用于管理 Azure 资源的跨平台命令行环境。</span><span class="sxs-lookup"><span data-stu-id="09429-113">The [Azure CLI](https://docs.microsoft.com/cli/azure?azure-portal=true) is Microsoft’s cross-platform command-line environment for managing Azure resources.</span></span> <span data-ttu-id="09429-114">您可以从浏览器使用 azure 云命令行管理程序, 也可以在 macOS、Linux 或 Windows 上本地安装 azure cli。</span><span class="sxs-lookup"><span data-stu-id="09429-114">You can use the Azure CLI from your browser with Azure Cloud Shell, or you can install the Azure CLI locally on macOS, Linux, or Windows.</span></span> <span data-ttu-id="09429-115">Azure CLI 是通过使用 bash 或 PowerShell 从本地命令行运行的。</span><span class="sxs-lookup"><span data-stu-id="09429-115">The Azure CLI is run from a local command line using bash or PowerShell.</span></span> <span data-ttu-id="09429-116">在本地运行 Azure CLI 需要额外的设置。</span><span class="sxs-lookup"><span data-stu-id="09429-116">Running the Azure CLI locally requires additional setup.</span></span> <span data-ttu-id="09429-117">我们将使用 azure 云命令行管理程序执行 azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="09429-117">We'll use Azure Cloud Shell for executing the Azure CLI commands.</span></span>

## <a name="what-is-azure-cloud-shell"></a><span data-ttu-id="09429-118">什么是 Azure 云命令行管理程序？</span><span class="sxs-lookup"><span data-stu-id="09429-118">What is Azure Cloud Shell?</span></span>

<span data-ttu-id="09429-119">Azure 云命令行管理程序是一个托管在云中的基于浏览器的命令行管理程序, 允许您使用经过身份验证的会话连接到 Azure。</span><span class="sxs-lookup"><span data-stu-id="09429-119">Azure Cloud Shell is a browser-based shell experience that's hosted in the cloud and allows you to connect to Azure using an authenticated session.</span></span> <span data-ttu-id="09429-120">您可以执行 azure CLI 命令, 以自动管理 PostgreSQL 服务器的 Azure 数据库。</span><span class="sxs-lookup"><span data-stu-id="09429-120">You can execute the Azure CLI commands to automate the management of an Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="09429-121">在云命令行管理程序中预安装并配置了常见的 Azure CLI 工具, 以便将其用于你的帐户。</span><span class="sxs-lookup"><span data-stu-id="09429-121">Common Azure CLI tools are pre-installed and configured in Cloud Shell for you to use with your account.</span></span>

> [!NOTE]
> <span data-ttu-id="09429-122">云命令行管理程序需要 Azure 存储资源, 以保留在云命令行管理程序中工作时创建的任何文件。</span><span class="sxs-lookup"><span data-stu-id="09429-122">Cloud Shell requires an Azure storage resource to persist any files you create while working in Cloud Shell.</span></span> <span data-ttu-id="09429-123">在首次启动时, 云命令行管理程序会代表你创建资源组、存储帐户和 Azure 文件共享。</span><span class="sxs-lookup"><span data-stu-id="09429-123">On first launch, Cloud Shell prompts to create a resource group, storage account, and Azure Files share on your behalf.</span></span> <span data-ttu-id="09429-124">这是一次性步骤, 将自动附加以供将来的所有云命令行管理器会话使用。</span><span class="sxs-lookup"><span data-stu-id="09429-124">This is a one-time step and will be automatically attached for all future Cloud Shell sessions.</span></span>

## <a name="create-an-azure-database-for-postgresql-server-using-the-azure-cli"></a><span data-ttu-id="09429-125">使用 azure CLI 为 PostgreSQL 服务器创建 Azure 数据库</span><span class="sxs-lookup"><span data-stu-id="09429-125">Create an Azure Database for PostgreSQL server using the Azure CLI</span></span>

<span data-ttu-id="09429-126">你将使用右侧的 azure 云命令行管理程序终端, 为使用 azure CLI 的 PostgreSQL 服务器创建 azure 数据库。</span><span class="sxs-lookup"><span data-stu-id="09429-126">You'll use the Azure Cloud Shell terminal on the right to create an Azure Database for PostgreSQL server using Azure CLI.</span></span>

<span data-ttu-id="09429-127">Azure CLI server 创建命令用法帮助显示所有可用参数, 如以下示例所示:</span><span class="sxs-lookup"><span data-stu-id="09429-127">The Azure CLI server creation command usage help showing all available parameters looks like the following example:</span></span>

```azurecli
az postgres server create [-h] [--verbose] [--debug]
                            [--output {json,jsonc,table,tsv}]
                            [--query JMESPATH]
                            --resource-group RESOURCE_GROUP_NAME --name SERVER_NAME
                            --sku-name SKU_NAME [--location LOCATION]
                            --admin-user ADMINISTRATOR_LOGIN
                            [--admin-password ADMINISTRATOR_LOGIN_PASSWORD]
                            [--backup-retention BACKUP_RETENTION]
                            [--geo-redundant-backup GEO_REDUNDANT_BACKUP]
                            [--ssl-enforcement {Enabled,Disabled}]
                            [--storage-size STORAGE_MB]
                            [--tags [TAGS [TAGS ...]]]
                            [--version VERSION]
                            [--subscription _SUBSCRIPTION]

```

<span data-ttu-id="09429-128">可选参数括在方括号中。</span><span class="sxs-lookup"><span data-stu-id="09429-128">The optional parameters are surrounded in brackets.</span></span> <span data-ttu-id="09429-129">让我们来看一下常见的一些常见情况。</span><span class="sxs-lookup"><span data-stu-id="09429-129">Let's examine a few of the common ones.</span></span>

### <a name="parameters"></a><span data-ttu-id="09429-130">参数</span><span class="sxs-lookup"><span data-stu-id="09429-130">Parameters</span></span>

<span data-ttu-id="09429-131">`--resource-group <resource_group_name>`参数指定要在其中创建服务器的资源组。</span><span class="sxs-lookup"><span data-stu-id="09429-131">The `--resource-group <resource_group_name>` parameter specifies the resource group within which to create the server.</span></span>

<span data-ttu-id="09429-132">您指定`admin-user`的`admin-password`服务器必须登录到服务器及其数据库。</span><span class="sxs-lookup"><span data-stu-id="09429-132">The server `admin-user` and `admin-password` that you specify is required to sign in to the server and its databases.</span></span> <span data-ttu-id="09429-133">请记住或记录此信息, 以便在以后与新服务器交互时使用。</span><span class="sxs-lookup"><span data-stu-id="09429-133">Remember or record this information for later when interacting with the new server.</span></span>

<span data-ttu-id="09429-134">您可以使用`--sku-name`参数指定定价层的一部分, 在此示例中为 "计算资源"。</span><span class="sxs-lookup"><span data-stu-id="09429-134">You use the `--sku-name` parameter to specify part of the pricing tier, in this case, compute resource.</span></span> <span data-ttu-id="09429-135">值遵循约定`{pricing tier}_{compute generation}_{vCores}`。</span><span class="sxs-lookup"><span data-stu-id="09429-135">The value follows the convention `{pricing tier}_{compute generation}_{vCores}`.</span></span>

<span data-ttu-id="09429-136">说明</span><span class="sxs-lookup"><span data-stu-id="09429-136">Examples:</span></span>

- <span data-ttu-id="09429-137">`--sku-name B_Gen4_4`映射到 Basic、Gen 4 和 4 vCores。</span><span class="sxs-lookup"><span data-stu-id="09429-137">`--sku-name B_Gen4_4` maps to Basic, Gen 4, and 4 vCores.</span></span>
- <span data-ttu-id="09429-138">`--sku-name GP_Gen5_32`映射到常规用途、第5代和 32 vCores。</span><span class="sxs-lookup"><span data-stu-id="09429-138">`--sku-name GP_Gen5_32` maps to General Purpose, Gen 5, and 32 vCores.</span></span>
- <span data-ttu-id="09429-139">`--sku-name MO_Gen5_2`映射到内存优化、第5代和第 2 vCores。</span><span class="sxs-lookup"><span data-stu-id="09429-139">`--sku-name MO_Gen5_2` maps to Memory Optimized, Gen 5, and 2 vCores.</span></span>

<span data-ttu-id="09429-140">回想一下, 我们在使用门户创建服务器的单位中讨论了这三个定价层。</span><span class="sxs-lookup"><span data-stu-id="09429-140">Recall that we discussed the three pricing tiers in the unit where we created the server using the portal.</span></span>

<span data-ttu-id="09429-141">假设您要使用基本、第5个和1个 vCore 计算资源。</span><span class="sxs-lookup"><span data-stu-id="09429-141">Let's assume you want to use a Basic, Gen 5, and 1 vCore compute resource.</span></span> <span data-ttu-id="09429-142">将参数指定为`--sku-name B_Gen5_1`。</span><span class="sxs-lookup"><span data-stu-id="09429-142">You'll specify the parameter as `--sku-name B_Gen5_1`.</span></span>

<span data-ttu-id="09429-143">您可以使用`--storage-size`参数指定定价层的一部分。</span><span class="sxs-lookup"><span data-stu-id="09429-143">You use the `--storage-size` parameter to specify part of the pricing tier.</span></span> <span data-ttu-id="09429-144">如果未指定值, 则默认为 5120 MB。</span><span class="sxs-lookup"><span data-stu-id="09429-144">If the value isn't specified, then it defaults to 5,120 MB.</span></span> <span data-ttu-id="09429-145">有效的存储大小范围为 5120 mb, 并以 1024 mb 增量增加到 1048576 mb。</span><span class="sxs-lookup"><span data-stu-id="09429-145">Valid storage sizes range from 5,120 MB and increases in increments of 1,024 MB up to 1,048,576 MB.</span></span>

<span data-ttu-id="09429-146">当`--backup-retention`您需要指定备份的保留期 (以天为单位指定) 时, 使用此参数。</span><span class="sxs-lookup"><span data-stu-id="09429-146">The `--backup-retention` parameter is used when you need to specify the retention period for backups, which is specified in days.</span></span> <span data-ttu-id="09429-147">如果未指定值, 则默认为七天。</span><span class="sxs-lookup"><span data-stu-id="09429-147">If the value isn't specified, then it defaults to seven days.</span></span>

<span data-ttu-id="09429-148">您可以使用`--version`参数指定要使用的 PostgreSQL 的主要版本。</span><span class="sxs-lookup"><span data-stu-id="09429-148">You use the `--version` parameter to specify the major version of PostgreSQL that you'd like to use.</span></span>

<span data-ttu-id="09429-149">现在, 您已看到使用 azure CLI 为 PostgreSQL 服务器创建 Azure 数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="09429-149">You've now seen the steps to create an Azure Database for PostgreSQL server using the Azure CLI.</span></span> <span data-ttu-id="09429-150">在下一个单元中, 你将使用 azure CLI 为 PostgreSQL 服务器创建 Azure 数据库。</span><span class="sxs-lookup"><span data-stu-id="09429-150">In the next unit, you'll create an Azure Database for PostgreSQL server using the Azure CLI.</span></span>