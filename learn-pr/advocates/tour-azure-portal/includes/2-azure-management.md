<span data-ttu-id="21530-101">您可以使用各种工具和平台配置和管理 Azure。</span><span class="sxs-lookup"><span data-stu-id="21530-101">You can configure and manage Azure using a broad range of tools and platforms.</span></span> <span data-ttu-id="21530-102">有一些工具可用于命令行、特定于语言的软件开发工具包 (sdk)、开发人员工具、用于迁移的工具和许多其他工具。</span><span class="sxs-lookup"><span data-stu-id="21530-102">There are tools available for the command line, language-specific Software Development Kits (SDKs), developer tools, tools for migration, and many others.</span></span> 

<span data-ttu-id="21530-103">日常管理和交互通常使用的工具包括:</span><span class="sxs-lookup"><span data-stu-id="21530-103">Tools that are commonly used for day-to-day management and interaction include:</span></span> 

- <span data-ttu-id="21530-104">**azure 门户**, 用于通过图形用户界面 (GUI) 与 Azure 进行交互</span><span class="sxs-lookup"><span data-stu-id="21530-104">**Azure portal** for interacting with Azure via a Graphical User Interface (GUI)</span></span>
- <span data-ttu-id="21530-105">**azure PowerShell**和**azure 命令行接口**(CLI), 用于命令行和与 azure 的基于自动化的交互</span><span class="sxs-lookup"><span data-stu-id="21530-105">**Azure PowerShell** and **Azure Command-Line Interface** (CLI) for command line and automation-based interactions with Azure</span></span>
- <span data-ttu-id="21530-106">基于 web 的命令行界面的**Azure 云**命令行管理程序</span><span class="sxs-lookup"><span data-stu-id="21530-106">**Azure Cloud Shell** for a web-based command-line interface</span></span>

<span data-ttu-id="21530-107">创建管理脚本和使用自动化工具是优化工作流的一种有效方式。</span><span class="sxs-lookup"><span data-stu-id="21530-107">Creating administration scripts and using automation tools is a powerful way to optimize your workflow.</span></span> <span data-ttu-id="21530-108">您可以自动执行重复的任务, 一旦脚本经过验证, 它将持续运行, 从而减少错误。</span><span class="sxs-lookup"><span data-stu-id="21530-108">You can automate repetitive tasks, and once a script has been verified, it will run consistently, thereby reducing errors.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="21530-109">Azure 门户</span><span class="sxs-lookup"><span data-stu-id="21530-109">Azure portal</span></span>

<span data-ttu-id="21530-110">Azure 门户是一个可通过 web 浏览器访问的网站, 可转到 URL [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="21530-110">The Azure portal is a website that you can access with a web browser, by going to the URL [https://portal.azure.com](https://portal.azure.com).</span></span> <span data-ttu-id="21530-111">从这里, 你可以手动与所有 Azure 服务交互。</span><span class="sxs-lookup"><span data-stu-id="21530-111">From here, you can interact manually with all the Azure services.</span></span> <span data-ttu-id="21530-112">您可以确定要查找的服务, 获取有关特定主题的帮助和更多学习的链接, 以及部署、管理和删除资源。</span><span class="sxs-lookup"><span data-stu-id="21530-112">You can identify a service you're looking for, get links for help and more learning on particular topics, and deploy, manage, and delete resources.</span></span> <span data-ttu-id="21530-113">此外, 它还将指导您使用向导和工具提示完成复杂的管理任务。</span><span class="sxs-lookup"><span data-stu-id="21530-113">It also guides you through complex administrative tasks using wizards and tooltips.</span></span>

<span data-ttu-id="21530-114">仪表板视图提供有关 Azure 环境的高级别详细信息。</span><span class="sxs-lookup"><span data-stu-id="21530-114">The dashboard view provides high-level details about your Azure environment.</span></span> <span data-ttu-id="21530-115">您可以根据需要, 通过移动和调整图块、显示感兴趣的特定服务、访问帮助和支持的链接以及提供反馈来自定义门户外观。</span><span class="sxs-lookup"><span data-stu-id="21530-115">You can customize the portal look as necessary by moving and resizing tiles, displaying particular services of interest, accessing links for help and support, and providing feedback.</span></span>

<span data-ttu-id="21530-116">门户不提供自动执行重复任务的任何方法。</span><span class="sxs-lookup"><span data-stu-id="21530-116">The portal does not provide any way to automate repetitive tasks.</span></span> <span data-ttu-id="21530-117">例如, 若要设置多个虚拟机, 您需要通过完成每个 vm 的向导一次创建一个虚拟机。</span><span class="sxs-lookup"><span data-stu-id="21530-117">For example, to set up multiple VMs, you would need to create them one at a time by completing the wizard for each VM.</span></span> <span data-ttu-id="21530-118">这使得门户方法非常耗时且容易出错, 从而实现复杂的任务。</span><span class="sxs-lookup"><span data-stu-id="21530-118">This makes the portal approach time-consuming and error-prone for complex tasks.</span></span>
 
 ## <a name="azure-powershell"></a><span data-ttu-id="21530-119">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="21530-119">Azure PowerShell</span></span>

<span data-ttu-id="21530-120">Azure PowerShell 是一个添加到 Windows PowerShell 或 PowerShell Core 的模块, 可让您连接到 Azure 订阅并管理资源。</span><span class="sxs-lookup"><span data-stu-id="21530-120">Azure PowerShell is a module that you add to Windows PowerShell or PowerShell Core that enables you to connect to your Azure subscription and manage resources.</span></span> <span data-ttu-id="21530-121">Azure PowerShell 需要 Windows PowerShell 才能正常工作。</span><span class="sxs-lookup"><span data-stu-id="21530-121">Azure PowerShell requires Windows PowerShell to function.</span></span> <span data-ttu-id="21530-122">PowerShell 提供命令行管理程序窗口和命令分析等服务。</span><span class="sxs-lookup"><span data-stu-id="21530-122">PowerShell provides services such as the shell window and command parsing.</span></span> <span data-ttu-id="21530-123">然后, azure PowerShell 将添加特定于 azure 的命令。</span><span class="sxs-lookup"><span data-stu-id="21530-123">Azure PowerShell then adds the Azure-specific commands.</span></span>

<span data-ttu-id="21530-124">例如, azure PowerShell 提供了在`New-AzureRmVM` Azure 订阅中为您创建虚拟机的命令。</span><span class="sxs-lookup"><span data-stu-id="21530-124">For example, Azure PowerShell provides the `New-AzureRmVM` command that creates a virtual machine for you inside your Azure subscription.</span></span> <span data-ttu-id="21530-125">若要使用它, 请启动 PowerShell, 使用命令`Connect-AzureRMAccount`登录 Azure 帐户, 然后发出如下命令:</span><span class="sxs-lookup"><span data-stu-id="21530-125">To use it, you would launch PowerShell, sign in to your Azure account using the command `Connect-AzureRMAccount`, and then issue a command such as:</span></span>

```powershell
New-AzureRmVm `
    -ResourceGroupName "MyResourceGroup" `
    -Name "TestVm" `
    -Image "UbuntuLTS"
    ...
```
> [!NOTE]
> <span data-ttu-id="21530-126">powershell Core 是运行在 Windows、Linux 或 macOS 上的跨平台版本的 powershell。</span><span class="sxs-lookup"><span data-stu-id="21530-126">PowerShell Core is a cross-platform version of PowerShell that runs on Windows, Linux or macOS.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="21530-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="21530-127">Azure CLI</span></span>

<span data-ttu-id="21530-128">azure CLI 是跨平台命令行程序, 它连接到 azure 并在 azure 资源上执行管理命令。</span><span class="sxs-lookup"><span data-stu-id="21530-128">Azure CLI is a cross-platform command-line program that connects to Azure and executes administrative commands on Azure resources.</span></span> <span data-ttu-id="21530-129">*跨平台*意味着它可以在 Windows、Linux 或 macOS 上运行。</span><span class="sxs-lookup"><span data-stu-id="21530-129">*Cross-platform* means that it can be run on Windows, Linux, or macOS.</span></span> <span data-ttu-id="21530-130">例如, 若要创建 VM, 请打开命令提示符窗口, 使用命令`az login`登录 Azure, 创建资源组, 然后使用类似如下的命令:</span><span class="sxs-lookup"><span data-stu-id="21530-130">For example, to create a VM, you would open a command prompt window, sign in to Azure using the command `az login`, create a resource group, then use a command such as:</span></span>

```azurecli
az vm create \
  --resource-group MyResourceGroup \
  --name TestVm \
  --image UbuntuLTS
  --generate-ssh-keys
  ...
```

## <a name="azure-cloud-shell"></a><span data-ttu-id="21530-131">Azure 云命令行管理程序</span><span class="sxs-lookup"><span data-stu-id="21530-131">Azure Cloud Shell</span></span>

<span data-ttu-id="21530-132">Azure 云命令行管理程序是门户中基于浏览器的脚本环境。</span><span class="sxs-lookup"><span data-stu-id="21530-132">Azure Cloud Shell is a browser-based scripting environment in your portal.</span></span> <span data-ttu-id="21530-133">它提供了选择最适合您工作方式的命令行管理程序体验的灵活性。</span><span class="sxs-lookup"><span data-stu-id="21530-133">It provides the flexibility of choosing the shell experience that best suits the way you work.</span></span> <span data-ttu-id="21530-134">Linux 用户可以选择获取 Bash 体验, 而 Windows 用户可以选择使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="21530-134">Linux users can opt for a Bash experience, while Windows users can opt for PowerShell.</span></span>

<span data-ttu-id="21530-135">azure 存储帐户是使用云命令行管理程序所必需的, 在访问 azure 云命令行管理程序时, 系统会提示你创建一个。</span><span class="sxs-lookup"><span data-stu-id="21530-135">An Azure storage account is required to use the cloud shell, and you will be prompted to create one when accessing the Azure cloud shell.</span></span>

<span data-ttu-id="21530-136">在 Microsoft 学习版中, 我们将使用云命令行管理程序来尝试使用 Azure 功能的许多交互式练习。</span><span class="sxs-lookup"><span data-stu-id="21530-136">In Microsoft Learn, we will use the Cloud Shell for many of the interactive exercises you will use to try out Azure features.</span></span>

> [!NOTE] 
> <span data-ttu-id="21530-137">你可以转到[https://shell.azure.com/](https://shell.azure.com/)访问 Azure 云命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="21530-137">You can access Azure Cloud Shell by going to [https://shell.azure.com/](https://shell.azure.com/).</span></span>

## <a name="other-options"></a><span data-ttu-id="21530-138">其他选项</span><span class="sxs-lookup"><span data-stu-id="21530-138">Other options</span></span>

<span data-ttu-id="21530-139">此外, 还有适用于一系列语言和框架的 Azure sdk, 以及可用于以编程方式管理和控制 Azure 资源的 REST api。</span><span class="sxs-lookup"><span data-stu-id="21530-139">There are also Azure SDKs for a range of languages and frameworks, as well as REST APIs that you can use to manage and control Azure resources programmatically.</span></span> <span data-ttu-id="21530-140">有关可用工具的完整列表, 请参阅[下载](https://azure.microsoft.com/en-us/downloads/)页面。</span><span class="sxs-lookup"><span data-stu-id="21530-140">For a full list of tools available, see the [Downloads](https://azure.microsoft.com/en-us/downloads/) page.</span></span>

<span data-ttu-id="21530-141">从 azure 开始时, 通常会使用 azure 门户。</span><span class="sxs-lookup"><span data-stu-id="21530-141">When starting with Azure, you will most often use the Azure portal.</span></span> <span data-ttu-id="21530-142">让我们进一步了解一下门户的方法。</span><span class="sxs-lookup"><span data-stu-id="21530-142">Let's take a closer look at the portal approach.</span></span>