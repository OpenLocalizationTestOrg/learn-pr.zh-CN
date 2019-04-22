<span data-ttu-id="927fe-101">假设您已选择 Azure PowerShell 作为自动化解决方案。</span><span class="sxs-lookup"><span data-stu-id="927fe-101">Suppose you have chosen Azure PowerShell as your automation solution.</span></span> <span data-ttu-id="927fe-102">您的管理员更愿意在本地运行脚本, 而不是在 Azure 云命令行管理程序中运行。</span><span class="sxs-lookup"><span data-stu-id="927fe-102">Your administrators prefer to run their scripts locally rather than in the Azure Cloud Shell.</span></span> <span data-ttu-id="927fe-103">团队使用运行 Linux、macOS 和 Windows 的计算机。</span><span class="sxs-lookup"><span data-stu-id="927fe-103">The team uses machines that run Linux, macOS, and Windows.</span></span> <span data-ttu-id="927fe-104">您需要让 Azure PowerShell 在其所有设备上正常工作。</span><span class="sxs-lookup"><span data-stu-id="927fe-104">You need to get Azure PowerShell working on all their devices.</span></span> 

## <a name="what-must-be-installed"></a><span data-ttu-id="927fe-105">必须安装哪些内容？</span><span class="sxs-lookup"><span data-stu-id="927fe-105">What must be installed?</span></span>
<span data-ttu-id="927fe-106">我们将在下一个单元中了解实际安装说明, 但我们来看一下组成 Azure PowerShell 的两个组件。</span><span class="sxs-lookup"><span data-stu-id="927fe-106">We'll go through the actual installation instructions in the next unit, but let's look at the two components which make up Azure PowerShell.</span></span>

- <span data-ttu-id="927fe-107">**基 PowerShell 产品**这有两种变种: 在 Windows 上为 powershell, 在 macOS 和 Linux 上为 powershell Core。</span><span class="sxs-lookup"><span data-stu-id="927fe-107">**The base PowerShell product** This comes in two variants: PowerShell on Windows, and PowerShell Core on macOS and Linux.</span></span>
- <span data-ttu-id="927fe-108">**Azure PowerShell 模块**必须安装此额外模块, 才能将特定于 Azure 的命令添加到 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="927fe-108">**The Azure PowerShell module** This extra module must be installed to add the Azure-specific commands to PowerShell.</span></span>

> [!TIP]
> <span data-ttu-id="927fe-109">PowerShell 包含在 Windows 中 (但可能有可用的更新)。</span><span class="sxs-lookup"><span data-stu-id="927fe-109">PowerShell is included with Windows (but might have an update available).</span></span> <span data-ttu-id="927fe-110">你将需要在 Linux 和 macOS 上安装 PowerShell Core。</span><span class="sxs-lookup"><span data-stu-id="927fe-110">You will need to install PowerShell Core on Linux and macOS.</span></span>

<span data-ttu-id="927fe-111">安装基本产品后, 即可将 Azure PowerShell 模块添加到安装中。</span><span class="sxs-lookup"><span data-stu-id="927fe-111">Once the base product is installed, you then add the Azure PowerShell module to your installation.</span></span>

## <a name="how-to-install-powershell-core"></a><span data-ttu-id="927fe-112">如何安装 PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="927fe-112">How to install PowerShell Core</span></span>
<span data-ttu-id="927fe-113">在 Linux 和 macOS 上, 使用程序包管理器安装 PowerShell Core。</span><span class="sxs-lookup"><span data-stu-id="927fe-113">On both Linux and macOS, you use a package manager to install PowerShell Core.</span></span> <span data-ttu-id="927fe-114">建议的程序包管理器因 OS 和分发而异。</span><span class="sxs-lookup"><span data-stu-id="927fe-114">The recommended package manager differs by OS and distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="927fe-115">PowerShell Core 在 Microsoft 存储库中可用, 因此你首先需要将该存储库添加到你的程序包管理器。</span><span class="sxs-lookup"><span data-stu-id="927fe-115">PowerShell Core is available in the Microsoft repository, so you'll first need to add that repository to your package manager.</span></span>

### <a name="linux"></a><span data-ttu-id="927fe-116">Linux</span><span class="sxs-lookup"><span data-stu-id="927fe-116">Linux</span></span>
<span data-ttu-id="927fe-117">在 linux 上, 程序包管理器将根据你选择的 Linux 分发进行更改。</span><span class="sxs-lookup"><span data-stu-id="927fe-117">On Linux, the package manager will change based on the Linux distribution you choose.</span></span>

| <span data-ttu-id="927fe-118">分发 (s)</span><span class="sxs-lookup"><span data-stu-id="927fe-118">Distribution(s)</span></span>  | <span data-ttu-id="927fe-119">程序包管理器</span><span class="sxs-lookup"><span data-stu-id="927fe-119">Package manager</span></span> |
|------------------|-----------------|
| <span data-ttu-id="927fe-120">Ubuntu、Debian</span><span class="sxs-lookup"><span data-stu-id="927fe-120">Ubuntu, Debian</span></span>   | `apt-get`       |
| <span data-ttu-id="927fe-121">Red Hat, CentOS</span><span class="sxs-lookup"><span data-stu-id="927fe-121">Red Hat, CentOS</span></span>  | `yum`           |
| <span data-ttu-id="927fe-122">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="927fe-122">OpenSUSE</span></span>         | `zypper`        |
| <span data-ttu-id="927fe-123">Fedora</span><span class="sxs-lookup"><span data-stu-id="927fe-123">Fedora</span></span>           | `dnf`           |

### <a name="mac"></a><span data-ttu-id="927fe-124">Mac</span><span class="sxs-lookup"><span data-stu-id="927fe-124">Mac</span></span>
<span data-ttu-id="927fe-125">在 macOS 上, 您将`Homebrew`使用安装 PowerShell Core。</span><span class="sxs-lookup"><span data-stu-id="927fe-125">On macOS, you will use `Homebrew` to install PowerShell Core.</span></span>

<span data-ttu-id="927fe-126">在下一节中, 您将完成一些常见平台的详细安装步骤。</span><span class="sxs-lookup"><span data-stu-id="927fe-126">In the next section, you will go through the detailed installation steps for some common platforms.</span></span>