<span data-ttu-id="50792-101">在此单元中, 将在本地计算机上安装**PowerShell** 。</span><span class="sxs-lookup"><span data-stu-id="50792-101">In this unit, you will install **PowerShell** on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="50792-102">本练习将指导您完成在本地安装 PowerShell 工具。</span><span class="sxs-lookup"><span data-stu-id="50792-102">This exercise guides you through installing the PowerShell tools locally.</span></span> <span data-ttu-id="50792-103">模块的其余部分将使用 Azure 云命令行管理程序, 以便你可以在 Microsoft 学习中利用免费订阅支持。</span><span class="sxs-lookup"><span data-stu-id="50792-103">The remainder of the module will use the Azure Cloud Shell so you can leverage the free subscription support in Microsoft Learn.</span></span> <span data-ttu-id="50792-104">您可以将此练习视为可选活动, 只需查看所需的说明即可。</span><span class="sxs-lookup"><span data-stu-id="50792-104">You can consider this exercise as an optional activity and just review the instructions if you prefer.</span></span>

::: zone pivot="linux"

## <a name="linux"></a><span data-ttu-id="50792-105">Linux</span><span class="sxs-lookup"><span data-stu-id="50792-105">Linux</span></span>

<span data-ttu-id="50792-106">为 Linux 安装 PowerShell 将涉及使用程序包管理器。</span><span class="sxs-lookup"><span data-stu-id="50792-106">Installing PowerShell for Linux will involve using a package manager.</span></span> <span data-ttu-id="50792-107">我们将在本示例中使用**Ubuntu 18.04** , 但我们的[文档中有其他版本和分发的详细说明](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux)。</span><span class="sxs-lookup"><span data-stu-id="50792-107">We will use **Ubuntu 18.04** for our example here, but we have [detailed instructions for other versions and distributions in our documentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

<span data-ttu-id="50792-108">您将使用高级打包工具 (**apt.**) 和 Bash 命令行在 Ubuntu Linux 上安装 PowerShell Core。</span><span class="sxs-lookup"><span data-stu-id="50792-108">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

1. <span data-ttu-id="50792-109">导入 Microsoft Ubuntu 存储库的加密密钥。</span><span class="sxs-lookup"><span data-stu-id="50792-109">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="50792-110">这将允许程序包管理器验证您安装的 PowerShell 核心包是否来自 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="50792-110">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. <span data-ttu-id="50792-111">注册**Microsoft Ubuntu 存储库**, 以便程序包管理器可以找到 PowerShell Core 程序包。</span><span class="sxs-lookup"><span data-stu-id="50792-111">Register the **Microsoft Ubuntu repository** so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="50792-112">更新程序包列表。</span><span class="sxs-lookup"><span data-stu-id="50792-112">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="50792-113">安装 PowerShell Core。</span><span class="sxs-lookup"><span data-stu-id="50792-113">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="50792-114">启动 PowerShell 以验证它是否已成功安装。</span><span class="sxs-lookup"><span data-stu-id="50792-114">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```
::: zone-end

::: zone pivot="macos"

## <a name="macos"></a><span data-ttu-id="50792-115">MacOS</span><span class="sxs-lookup"><span data-stu-id="50792-115">MacOS</span></span>

<span data-ttu-id="50792-116">在 macOS 上, 第一步是安装**PowerShell Core**。</span><span class="sxs-lookup"><span data-stu-id="50792-116">On macOS, the first step is to install **PowerShell Core**.</span></span> <span data-ttu-id="50792-117">这是使用 Homebrew 程序包管理器完成的。</span><span class="sxs-lookup"><span data-stu-id="50792-117">This is done using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50792-118">如果**brew**命令不可用, 则可能需要安装 Homebrew 程序包管理器。</span><span class="sxs-lookup"><span data-stu-id="50792-118">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="50792-119">有关详细信息, 请参阅[Homebrew 网站](https://brew.sh/)。</span><span class="sxs-lookup"><span data-stu-id="50792-119">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="50792-120">安装 Homebrew-Cask 以获取更多程序包, 包括 PowerShell Core 程序包:</span><span class="sxs-lookup"><span data-stu-id="50792-120">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```

1. <span data-ttu-id="50792-121">安装 PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="50792-121">Install PowerShell Core:</span></span>

    ```bash
    brew cask install powershell
    ```

1. <span data-ttu-id="50792-122">启动 PowerShell Core 以验证它是否已成功安装:</span><span class="sxs-lookup"><span data-stu-id="50792-122">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

::: zone-end

::: zone pivot="windows"

## <a name="windows"></a><span data-ttu-id="50792-123">Windows</span><span class="sxs-lookup"><span data-stu-id="50792-123">Windows</span></span>
<span data-ttu-id="50792-124">PowerShell 包含在 Windows 中, 但可能存在适用于您的计算机的更新。</span><span class="sxs-lookup"><span data-stu-id="50792-124">PowerShell is included with Windows, however there may be an update available for your machine.</span></span> <span data-ttu-id="50792-125">我们打算使用的 Azure 支持需要 PowerShell 版本5.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="50792-125">The Azure support we are going to use requires PowerShell version 5.0 or higher.</span></span> <span data-ttu-id="50792-126">您可以通过以下步骤检查已安装的版本:</span><span class="sxs-lookup"><span data-stu-id="50792-126">You can check the version you have installed through the following steps:</span></span>

1. <span data-ttu-id="50792-127">打开 "**开始**" 菜单并键入**Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="50792-127">Open the **Start** menu and type **Windows PowerShell**.</span></span> <span data-ttu-id="50792-128">可能有多个可用的快捷方式链接:</span><span class="sxs-lookup"><span data-stu-id="50792-128">There may be multiple shortcut links available:</span></span>
    - <span data-ttu-id="50792-129">Windows PowerShell-这是64位版本, 通常是应选择的内容。</span><span class="sxs-lookup"><span data-stu-id="50792-129">Windows PowerShell - this is the 64-bit version and generally what you should choose.</span></span>
    - <span data-ttu-id="50792-130">Windows PowerShell (x86)-这是在64位 Windows 上安装的32位版本。</span><span class="sxs-lookup"><span data-stu-id="50792-130">Windows PowerShell (x86) - this is a 32-bit version installed on 64-bit Windows.</span></span>
    - <span data-ttu-id="50792-131">Windows PowerShell ISE-集成脚本环境 (ISE) 用于在 PowerShell 中编写脚本。</span><span class="sxs-lookup"><span data-stu-id="50792-131">Windows PowerShell ISE - The Integrated Scripting Environment (ISE) is used for writing scripts in PowerShell.</span></span> 
    - <span data-ttu-id="50792-132">Windows PowerShell ISE (x86)-32 位版本的 ISE。</span><span class="sxs-lookup"><span data-stu-id="50792-132">Windows PowerShell ISE (x86) - A 32-bit version of the ISE.</span></span>

1. <span data-ttu-id="50792-133">选择 "Windows PowerShell" 图标。</span><span class="sxs-lookup"><span data-stu-id="50792-133">Select the Windows PowerShell icon.</span></span>

1. <span data-ttu-id="50792-134">键入以下命令, 以确定安装的 PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="50792-134">Type the following command to determine the version of PowerShell installed.</span></span>

    ```powershell
    $PSVersionTable.PSVersion
    ```
    
<span data-ttu-id="50792-135">如果版本号低于 5.0, 请按照这些说明[升级现有 Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell)。</span><span class="sxs-lookup"><span data-stu-id="50792-135">If the version number is lower than 5.0, follow these instructions for [upgrading existing Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

::: zone-end

<span data-ttu-id="50792-136">您已将本地计算机设置为支持 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="50792-136">You have setup your local machine(s) to support PowerShell.</span></span> <span data-ttu-id="50792-137">接下来, 我们将讨论你可以添加的其他命令, 包括 Azure 模块。</span><span class="sxs-lookup"><span data-stu-id="50792-137">Next, we will talk about additional commands you can add including the Azure module.</span></span>