<span data-ttu-id="f0fce-101">让我们在您的本地计算机上安装 Azure CLI, 然后运行命令来验证您的安装。</span><span class="sxs-lookup"><span data-stu-id="f0fce-101">Let's install the Azure CLI on your local machine, and then run a command to verify your installation.</span></span> <span data-ttu-id="f0fce-102">您用于安装 Azure CLI 的方法取决于您的计算机的操作系统。</span><span class="sxs-lookup"><span data-stu-id="f0fce-102">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="f0fce-103">选择适用于您的操作系统的步骤。</span><span class="sxs-lookup"><span data-stu-id="f0fce-103">Choose the steps for your operating system.</span></span>

> [!NOTE]
> <span data-ttu-id="f0fce-104">本练习将指导您在本地安装 Azure CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="f0fce-104">This exercise guides you through installing the Azure CLI tool locally.</span></span> <span data-ttu-id="f0fce-105">模块的其余部分将使用 Azure 云命令行管理程序, 以便你可以在 Microsoft 学习中利用免费订阅支持。</span><span class="sxs-lookup"><span data-stu-id="f0fce-105">The remainder of the module will use the Azure Cloud Shell so you can leverage the free subscription support in Microsoft Learn.</span></span> <span data-ttu-id="f0fce-106">您可以将此练习视为可选活动, 只需查看所需的说明即可。</span><span class="sxs-lookup"><span data-stu-id="f0fce-106">You can consider this exercise as an optional activity and just review the instructions if you prefer.</span></span>

::: zone pivot="linux"

## <a name="linux"></a><span data-ttu-id="f0fce-107">Linux</span><span class="sxs-lookup"><span data-stu-id="f0fce-107">Linux</span></span>

<span data-ttu-id="f0fce-108">在这里, 你将使用高级打包工具 (**apt.**) 和 Bash 命令行在**Ubuntu Linux**上安装 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f0fce-108">Here you will install the Azure CLI on **Ubuntu Linux** using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!TIP]
> <span data-ttu-id="f0fce-109">下面列出的命令适用于 Ubuntu 版本18.04。</span><span class="sxs-lookup"><span data-stu-id="f0fce-109">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="f0fce-110">其他版本和 linux 的分发有不同的说明。</span><span class="sxs-lookup"><span data-stu-id="f0fce-110">Other versions and distributions of Linux have different instructions.</span></span> <span data-ttu-id="f0fce-111">如果您使用的是其他 Linux 版本, 请查看[官方文档](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f0fce-111">Check the [official documentation](https://docs.microsoft.com/cli/azure/install-azure-cli) if you are using a different Linux version.</span></span>

1. <span data-ttu-id="f0fce-112">修改源列表以注册 Microsoft 存储库, 并且程序包管理器可以找到 Azure CLI 程序包。</span><span class="sxs-lookup"><span data-stu-id="f0fce-112">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```

1. <span data-ttu-id="f0fce-113">导入 Microsoft Ubuntu 存储库的加密密钥。</span><span class="sxs-lookup"><span data-stu-id="f0fce-113">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="f0fce-114">这将允许程序包管理器验证您安装的 Azure CLI 程序包是否来自 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="f0fce-114">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. <span data-ttu-id="f0fce-115">安装 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f0fce-115">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

::: zone-end

::: zone pivot="macos"

## <a name="macos"></a><span data-ttu-id="f0fce-116">macOS</span><span class="sxs-lookup"><span data-stu-id="f0fce-116">macOS</span></span>

<span data-ttu-id="f0fce-117">在这里, 将使用 Homebrew 程序包管理器在 macOS 上安装 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f0fce-117">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0fce-118">如果**brew**命令不可用, 则可能需要安装 Homebrew 程序包管理器。</span><span class="sxs-lookup"><span data-stu-id="f0fce-118">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="f0fce-119">有关详细信息, 请参阅[Homebrew 网站](https://brew.sh/)。</span><span class="sxs-lookup"><span data-stu-id="f0fce-119">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="f0fce-120">更新你的 brew 存储库以确保你获取最新的 Azure CLI 程序包。</span><span class="sxs-lookup"><span data-stu-id="f0fce-120">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```

1. <span data-ttu-id="f0fce-121">安装 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f0fce-121">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

::: zone-end

::: zone pivot="windows"

## <a name="windows"></a><span data-ttu-id="f0fce-122">Windows</span><span class="sxs-lookup"><span data-stu-id="f0fce-122">Windows</span></span>

<span data-ttu-id="f0fce-123">在这里, 你将使用 MSI 安装程序在 Windows 上安装 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f0fce-123">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="f0fce-124">转到[https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), 并在 "浏览器安全性" 对话框中, 单击 "**运行**"。</span><span class="sxs-lookup"><span data-stu-id="f0fce-124">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="f0fce-125">在安装程序中, 接受许可条款, 然后单击 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="f0fce-125">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="f0fce-126">在 "**用户帐户控制**" 对话框中, 选择 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="f0fce-126">In the **User Account Control** dialog, select **Yes**.</span></span>

::: zone-end

## <a name="running-the-azure-cli"></a><span data-ttu-id="f0fce-127">运行 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f0fce-127">Running the Azure CLI</span></span>

<span data-ttu-id="f0fce-128">您可以通过打开 bash 命令行管理程序 (Linux 和 macOS) 或命令提示符或 PowerShell (Windows) 来运行 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f0fce-128">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="f0fce-129">启动 Azure CLI, 并通过运行版本检查来验证您的安装。</span><span class="sxs-lookup"><span data-stu-id="f0fce-129">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```azurecli
    az --version
    ```

::: zone pivot="windows"

> [!TIP]
> <span data-ttu-id="f0fce-130">从 PowerShell 运行 azure cli 与从 Windows 命令提示符运行 azure cli 有一些优势。</span><span class="sxs-lookup"><span data-stu-id="f0fce-130">Running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the Windows command prompt.</span></span> <span data-ttu-id="f0fce-131">PowerShell 通过命令提示符处提供的其他选项卡完成功能。</span><span class="sxs-lookup"><span data-stu-id="f0fce-131">PowerShell provides additional tab completion features over those available from the command prompt.</span></span>

::: zone-end

<span data-ttu-id="f0fce-132">你将本地计算机设置为使用 azure CLI 管理 azure 资源。</span><span class="sxs-lookup"><span data-stu-id="f0fce-132">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="f0fce-133">现在, 您可以在本地使用 Azure CLI 输入命令或执行脚本。</span><span class="sxs-lookup"><span data-stu-id="f0fce-133">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="f0fce-134">azure CLI 将你的命令转发到 azure 数据中心, 以在 azure 订阅中运行它们。</span><span class="sxs-lookup"><span data-stu-id="f0fce-134">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>