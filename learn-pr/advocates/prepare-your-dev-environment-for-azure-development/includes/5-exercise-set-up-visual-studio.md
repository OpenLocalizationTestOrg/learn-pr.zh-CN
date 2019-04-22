<span data-ttu-id="4b84b-101">在这里, 你将在 Windows 或 macOS 开发计算机上安装 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4b84b-101">Here, you'll install Visual Studio on either your Windows or your macOS development machine.</span></span>

## <a name="exercise-steps"></a><span data-ttu-id="4b84b-102">练习步骤</span><span class="sxs-lookup"><span data-stu-id="4b84b-102">Exercise steps</span></span>

::: zone pivot="windows"

### <a name="windows"></a><span data-ttu-id="4b84b-103">Windows</span><span class="sxs-lookup"><span data-stu-id="4b84b-103">Windows</span></span>

1. <span data-ttu-id="4b84b-104">从https://visualstudio.microsoft.com/downloads/下载 Visual Studio 安装程序。</span><span class="sxs-lookup"><span data-stu-id="4b84b-104">Download the Visual Studio installer from https://visualstudio.microsoft.com/downloads/.</span></span>

1. <span data-ttu-id="4b84b-105">运行安装程序。</span><span class="sxs-lookup"><span data-stu-id="4b84b-105">Run the installer.</span></span>

1. <span data-ttu-id="4b84b-106">在 "**工作负荷**" 选项卡上, 选择**Azure 开发**工作负载。</span><span class="sxs-lookup"><span data-stu-id="4b84b-106">On the **Workloads** tab, select the **Azure development** workload.</span></span>

    <span data-ttu-id="4b84b-107">下面的屏幕截图显示了在 visual studio 中选择允许 Azure 开发的 visual studio 安装程序工作负荷。</span><span class="sxs-lookup"><span data-stu-id="4b84b-107">The following screenshot shows the Visual Studio Installer workload selected to allow Azure development within Visual Studio.</span></span>

    ![突出显示了 Azure 开发工作负载的 Visual Studio 安装程序的屏幕截图。](../media/5-select-azure-workload.png)

1. <span data-ttu-id="4b84b-109">Optional安装 ASP.NET 和 web 开发工作负载, 准备好创建适用于 Azure 的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="4b84b-109">(Optional) Install the ASP.NET and web development workload to be ready to create web applications for Azure.</span></span>

1. <span data-ttu-id="4b84b-110">单击 "**安装**", 等待 Visual Studio 安装。</span><span class="sxs-lookup"><span data-stu-id="4b84b-110">Click **Install**, and wait for Visual Studio to install.</span></span> <span data-ttu-id="4b84b-111">对于已安装 Visual Studio 的系统, 此按钮可能会显示 "**修改**"。</span><span class="sxs-lookup"><span data-stu-id="4b84b-111">For systems with Visual Studio already installed, this button may say **Modify**.</span></span>

1. <span data-ttu-id="4b84b-112">安装完成后, 打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4b84b-112">When the installation is complete, open Visual Studio.</span></span>

1. <span data-ttu-id="4b84b-113">转到 Visual Studio 中的 "视图" 菜单, 确保您具有 "**云资源管理器**" 选项。</span><span class="sxs-lookup"><span data-stu-id="4b84b-113">Go to the View menu in Visual Studio and make sure you have the **Cloud Explorer** option.</span></span>

    <span data-ttu-id="4b84b-114">下面的屏幕截图显示了在安装了 Azure 开发工作负载时将显示的云浏览器菜单选项。</span><span class="sxs-lookup"><span data-stu-id="4b84b-114">The following screenshot shows the Cloud Explorer menu option that will be present if you have the Azure development workload installed.</span></span>

    ![突出显示了 "云浏览器" 菜单选项的 Visual Studio "视图" 菜单屏幕截图。](../media/5-verify-cloud-explorer.png)

::: zone-end

::: zone pivot="macos"

### <a name="macos"></a><span data-ttu-id="4b84b-116">macOS</span><span class="sxs-lookup"><span data-stu-id="4b84b-116">macOS</span></span>

1. <span data-ttu-id="4b84b-117">转到https://visualstudio.microsoft.com/并下载 Visual Studio for Mac 安装程序。</span><span class="sxs-lookup"><span data-stu-id="4b84b-117">Go to https://visualstudio.microsoft.com/ and download the Visual Studio for Mac installer.</span></span>

1. <span data-ttu-id="4b84b-118">单击 VisualStudioInstaller 文件以装入安装程序, 然后通过双击徽标运行它。</span><span class="sxs-lookup"><span data-stu-id="4b84b-118">Click the VisualStudioInstaller.dmg file to mount the installer, then run it by double-clicking the logo.</span></span>

1. <span data-ttu-id="4b84b-119">在出现时确认隐私和许可条款。</span><span class="sxs-lookup"><span data-stu-id="4b84b-119">Acknowledge the Privacy and License terms when presented.</span></span>

1. <span data-ttu-id="4b84b-120">安装程序将询问您要安装哪些组件。</span><span class="sxs-lookup"><span data-stu-id="4b84b-120">The installer will ask which components you wish to install.</span></span> <span data-ttu-id="4b84b-121">Azure 组件已经是 Visual Studio for Mac 的一部分, 但建议安装 **.net Core** platform 以开发适用于 Azure 的 web 体验。</span><span class="sxs-lookup"><span data-stu-id="4b84b-121">Azure components are already part of Visual Studio for Mac, but it is recommended to install the **.NET Core** platform to develop web experiences for Azure.</span></span>

    <span data-ttu-id="4b84b-122">下面的屏幕截图显示了向 Visual Studio for Mac 添加 Azure 开发功能所需的 .net 核心平台。</span><span class="sxs-lookup"><span data-stu-id="4b84b-122">The following screenshot shows the .NET Core platform required to add Azure development capabilities to Visual Studio for Mac.</span></span>

    ![突出显示了选定的 .net Core platform 选项的 Visual Studio for Mac 安装程序的屏幕截图。](../media/5-vsmac-install-net-core.png)

1. <span data-ttu-id="4b84b-124">选择好选择后, 单击 "**安装并更新**", 并等待安装程序完成。</span><span class="sxs-lookup"><span data-stu-id="4b84b-124">Click **Install and Update** once you are happy with the selections, and wait for the installer to complete.</span></span>

1. <span data-ttu-id="4b84b-125">如果系统提示你提升所需的权限, 请使用管理员凭据执行此操作。</span><span class="sxs-lookup"><span data-stu-id="4b84b-125">If you are prompted to elevate the permissions needed, use your administrator credentials to do so.</span></span>

1. <span data-ttu-id="4b84b-126">安装程序完成后, 启动 Visual Studio for Mac。</span><span class="sxs-lookup"><span data-stu-id="4b84b-126">Once the installer is complete, start Visual Studio for Mac.</span></span>

::: zone-end