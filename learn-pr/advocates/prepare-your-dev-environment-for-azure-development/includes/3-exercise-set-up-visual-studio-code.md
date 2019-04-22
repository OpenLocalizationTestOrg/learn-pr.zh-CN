<span data-ttu-id="2de33-101">若要将 visual studio code 用于 Azure 开发, 需要在本地安装 visual studio code 和一个或多个 azure 扩展。</span><span class="sxs-lookup"><span data-stu-id="2de33-101">To use Visual Studio Code for Azure development, you'll need to install Visual Studio Code locally and one or more Azure extensions.</span></span> <span data-ttu-id="2de33-102">在本练习中, 我们将添加**Azure 应用服务**扩展。</span><span class="sxs-lookup"><span data-stu-id="2de33-102">In this exercise, we'll add the **Azure App Service** extension.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2de33-103">安装 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2de33-103">Install Visual Studio Code</span></span>

::: zone pivot="windows"

### <a name="windows"></a><span data-ttu-id="2de33-104">Windows</span><span class="sxs-lookup"><span data-stu-id="2de33-104">Windows</span></span>

1. <span data-ttu-id="2de33-105">[下载 Visual Studio Code installer for Windows](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="2de33-105">[Download the Visual Studio Code installer for Windows](https://code.visualstudio.com/).</span></span>

1. <span data-ttu-id="2de33-106">运行安装程序。</span><span class="sxs-lookup"><span data-stu-id="2de33-106">Run the installer.</span></span>

1. <span data-ttu-id="2de33-107">打开 visual studio code, 方法是按 Windows 键或单击任务栏上的 "Windows" 图标, 键入 "visual studio code" 并单击**visual studio code** result。</span><span class="sxs-lookup"><span data-stu-id="2de33-107">Open Visual Studio Code by pressing the Windows key or clicking the Windows icon on the task bar, typing "Visual Studio Code" and clicking on the **Visual Studio Code** result.</span></span>

::: zone-end

::: zone pivot="macos"

### <a name="macos"></a><span data-ttu-id="2de33-108">macOS</span><span class="sxs-lookup"><span data-stu-id="2de33-108">macOS</span></span>

1. <span data-ttu-id="2de33-109">[下载 macOS 的 Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="2de33-109">[Download Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span>

1. <span data-ttu-id="2de33-110">双击下载的存档以展开内容。</span><span class="sxs-lookup"><span data-stu-id="2de33-110">Double-click on the downloaded archive to expand the contents.</span></span>

1. <span data-ttu-id="2de33-111">将 Visual Studio Code. app 拖到应用程序文件夹。</span><span class="sxs-lookup"><span data-stu-id="2de33-111">Drag Visual Studio Code.app to the Applications folder.</span></span>

1. <span data-ttu-id="2de33-112">通过单击图标 "应用" 部分或通过在 "聚光灯" 中搜索 Visual studio code 来打开 visual studio code。</span><span class="sxs-lookup"><span data-stu-id="2de33-112">Open Visual Studio Code by clicking on the icon the Apps section or by searching for Visual Studio Code in Spotlight.</span></span>

::: zone-end

::: zone pivot="linux"

### <a name="linux"></a><span data-ttu-id="2de33-113">Linux</span><span class="sxs-lookup"><span data-stu-id="2de33-113">Linux</span></span> 

#### <a name="debian-and-ubuntu"></a><span data-ttu-id="2de33-114">Debian 和 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2de33-114">Debian and Ubuntu</span></span>

1. <span data-ttu-id="2de33-115">下载并安装[deb 程序包 (64-bit)](https://go.microsoft.com/fwlink/?LinkID=760868) (如果可用) 或通过命令行 (替换为下载的. deb 文件名) 中的图形`<file>`软件中心 (替换为. filename):</span><span class="sxs-lookup"><span data-stu-id="2de33-115">Download and install the [.deb package (64-bit)](https://go.microsoft.com/fwlink/?LinkID=760868) through the graphical software center, if it's available, or through the command line (replacing `<file>` with the .deb filename you downloaded):</span></span>

    ```bash
    sudo dpkg -i <file>.deb
    sudo apt-get install -f # Install dependencies
    ```

#### <a name="rhel-fedora-and-centos"></a><span data-ttu-id="2de33-116">RHEL、Fedora 和 CentOS</span><span class="sxs-lookup"><span data-stu-id="2de33-116">RHEL, Fedora, and CentOS</span></span>

1. <span data-ttu-id="2de33-117">使用以下脚本安装密钥和存储库:</span><span class="sxs-lookup"><span data-stu-id="2de33-117">Use the following script to install the key and repository:</span></span>

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    ```

1. <span data-ttu-id="2de33-118">更新包缓存, 并使用 dnf (Fedora 22 及更高版本) 安装程序包:</span><span class="sxs-lookup"><span data-stu-id="2de33-118">Update the package cache, and install the package by using dnf (Fedora 22 and above):</span></span>

    ```bash
    dnf check-update
    sudo dnf install code
    ```

#### <a name="opensuse-and-sle"></a><span data-ttu-id="2de33-119">openSUSE 和 SLE</span><span class="sxs-lookup"><span data-stu-id="2de33-119">openSUSE and SLE</span></span>

1. <span data-ttu-id="2de33-120">yum 存储库还适用于基于 openSUSE 和 SLE 的系统。</span><span class="sxs-lookup"><span data-stu-id="2de33-120">The yum repository also works for openSUSE and SLE based systems.</span></span> <span data-ttu-id="2de33-121">下面的脚本将安装密钥和存储库:</span><span class="sxs-lookup"><span data-stu-id="2de33-121">The following script will install the key and repository:</span></span>

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
    ```

1. <span data-ttu-id="2de33-122">使用以下内容更新包缓存并安装包:</span><span class="sxs-lookup"><span data-stu-id="2de33-122">Update the package cache and install the package by using:</span></span>

    ```bash
    sudo zypper refresh
    sudo zypper install code
    ```

> [!NOTE]
> <span data-ttu-id="2de33-123">有关在各种 Linux 分发上安装或更新 Visual studio code 的详细信息, 请参阅在[linux 文档中运行 visual studio code](https://code.visualstudio.com/docs/setup/linux)。</span><span class="sxs-lookup"><span data-stu-id="2de33-123">For further details about installing or updating Visual Studio Code on various Linux distributions, please see the [Running Visual Studio Code on Linux documentation](https://code.visualstudio.com/docs/setup/linux).</span></span>

::: zone-end

## <a name="install-azure-app-service-extension"></a><span data-ttu-id="2de33-124">安装 Azure 应用服务扩展</span><span class="sxs-lookup"><span data-stu-id="2de33-124">Install Azure App Service extension</span></span>

1. <span data-ttu-id="2de33-125">如果尚未打开, 请打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="2de33-125">If you haven't already, open Visual Studio Code.</span></span>

1. <span data-ttu-id="2de33-126">打开扩展浏览器;它通过左侧的菜单进行访问。</span><span class="sxs-lookup"><span data-stu-id="2de33-126">Open the Extensions browser; it's accessed via the menu on the left.</span></span>

1. <span data-ttu-id="2de33-127">搜索**Azure 应用服务**。</span><span class="sxs-lookup"><span data-stu-id="2de33-127">Search for **Azure App Service**.</span></span>

1. <span data-ttu-id="2de33-128">选择 " **Azure 应用服务**结果", 然后单击 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="2de33-128">Select the **Azure App Service** result and click **Install**.</span></span>

    <span data-ttu-id="2de33-129">下面的屏幕截图显示了从 Visual Studio Code extension 搜索结果中选择的 Azure 应用服务扩展。</span><span class="sxs-lookup"><span data-stu-id="2de33-129">The following screenshot shows the Azure App Service extension selected from the Visual Studio Code extension search results.</span></span>

    ![显示在搜索结果中突出显示了 Azure 应用服务扩展的 "扩展" 选项卡的 Visual Studio 代码的屏幕截图。](../media/3-install-azure-extension.png)

<span data-ttu-id="2de33-131">这将安装扩展。</span><span class="sxs-lookup"><span data-stu-id="2de33-131">This will install the extension.</span></span> <span data-ttu-id="2de33-132">现已准备好连接到 azure 订阅, 并将 web、移动或 API 应用程序部署到 azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="2de33-132">You're now ready to connect to your Azure subscription and deploy a web, mobile, or API app to an Azure App Service.</span></span>
