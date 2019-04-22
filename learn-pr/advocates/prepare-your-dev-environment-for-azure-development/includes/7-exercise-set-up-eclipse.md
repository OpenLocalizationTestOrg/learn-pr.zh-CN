<span data-ttu-id="b6ce2-101">在这里, 你将在开发计算机上安装 Eclipse 和 Azure 工具包。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-101">Here you'll install Eclipse and the Azure Toolkit on your development machine.</span></span> <span data-ttu-id="b6ce2-102">在练习的最后, 你将拥有创建连接到 Azure 的 Java 应用程序所需的一切。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-102">By the end of the exercise, you'll have everything you need to create a Java application connected to Azure.</span></span>

## <a name="install-eclipse-ide"></a><span data-ttu-id="b6ce2-103">安装日蚀式 IDE</span><span class="sxs-lookup"><span data-stu-id="b6ce2-103">Install Eclipse IDE</span></span>

1. <span data-ttu-id="b6ce2-104">下载适用[于您的操作系统的 Eclipse IDE](https://www.eclipse.org/downloads/packages/installer)。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-104">Download the appropriate [Eclipse IDE for your operating system](https://www.eclipse.org/downloads/packages/installer).</span></span>

1. <span data-ttu-id="b6ce2-105">下载 Eclipse 安装程序后启动。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-105">Start the Eclipse installer once downloaded.</span></span>

    1. <span data-ttu-id="b6ce2-106">在 Windows 上, 双击下载的文件。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-106">On Windows, double-click the downloaded file.</span></span>

    1. <span data-ttu-id="b6ce2-107">在 macOS 和 Linux 上, 从下载的文件中解压缩安装程序并运行它。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-107">On macOS and Linux, unzip the installer from the downloaded file and run it.</span></span>

        > [!NOTE]
        > <span data-ttu-id="b6ce2-108">如果缺少 Java 开发工具包, 安装程序可能会提示您安装它。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-108">The installer may prompt you to install the Java Development Kit, if it is missing.</span></span>

1. <span data-ttu-id="b6ce2-109">选择要安装的程序包。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-109">Select the packages to install.</span></span> <span data-ttu-id="b6ce2-110">对于 java 开发人员, 选择 java 或 java EE 日蚀式 IDE 选项。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-110">For Java developers, choose either the Java or Java EE Eclipse IDE option.</span></span>

1. <span data-ttu-id="b6ce2-111">选择您的计算机上的安装目标。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-111">Select the installation destination on your machine.</span></span>

1. <span data-ttu-id="b6ce2-112">启动 Eclipse 以验证它是否已正确安装。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-112">Launch Eclipse to validate that it installed correctly.</span></span>

## <a name="install-azure-toolkit-for-eclipse"></a><span data-ttu-id="b6ce2-113">为 Eclipse 安装 Azure 工具包</span><span class="sxs-lookup"><span data-stu-id="b6ce2-113">Install Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="b6ce2-114">安装 Azure 工具包在 Windows、macOS 和 Linux 中是相同的。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-114">Installing the Azure Toolkit is the same across Windows, macOS, and Linux.</span></span>

1. <span data-ttu-id="b6ce2-115">启动 Eclipse。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-115">Start Eclipse.</span></span>

1. <span data-ttu-id="b6ce2-116">转到 "**帮助** > **安装新软件 ...**"。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-116">Go to **Help** > **Install New Software...**.</span></span>

    <span data-ttu-id="b6ce2-117">下面的屏幕截图显示了 "**安装新软件 ...** " 项的菜单位置。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-117">The following screenshot shows the menu location of the **Install New Software...** item.</span></span>

    ![在日蚀的帮助菜单中突出显示了 "安装新软件" 选项的屏幕截图。](../media/7-eclipse-install-new-software.png)

1. <span data-ttu-id="b6ce2-119">将会打开 "**可用软件**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-119">The **Available Software** dialog will open.</span></span> <span data-ttu-id="b6ce2-120">在 "**工作方式:** " 文本框中, `http://dl.microsoft.com/eclipse/`键入, 然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-120">In the **Work with:** text box, type `http://dl.microsoft.com/eclipse/` and press Enter.</span></span>

1. <span data-ttu-id="b6ce2-121">在结果中, 查看 "**适用于 Java 的 Azure 工具包**" 选项。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-121">In the results, check the **Azure Toolkit for Java** option.</span></span> <span data-ttu-id="b6ce2-122">确保在 "**安装过程中对所有更新网站进行更新以查找所需的软件**" 选项 (如果尚未选中)。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-122">Make sure you uncheck the **Contact all update sites during install to find required software** option, if it isn't already.</span></span>

    <span data-ttu-id="b6ce2-123">下面的屏幕截图显示了**可用的软件**安装配置, 如上文所述。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-123">The following screenshot shows the **Available Software** install configuration as described above.</span></span>

    ![Eclipse 中的 "可用软件" 窗口的屏幕截图, 框突出显示了查找和安装适用于 Java 的 Azure 工具包所需的配置。](../media/7-eclipse-download-azure-toolkit-for-java.png)

1. <span data-ttu-id="b6ce2-125">单击"下一步"。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-125">Click **Next**.</span></span>

1. <span data-ttu-id="b6ce2-126">在收到提示时查看并接受许可协议, 然后单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-126">Review and accept the license agreements when prompted, and click **Finish**.</span></span>

1. <span data-ttu-id="b6ce2-127">日蚀将下载并安装 Azure 工具包。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-127">Eclipse will download and install the Azure Toolkit.</span></span>

1. <span data-ttu-id="b6ce2-128">如果需要, 请重新启动 Eclipse。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-128">Restart Eclipse if required.</span></span>

1. <span data-ttu-id="b6ce2-129">验证是否可以在 Eclipse 中找到\*\*\*\* > "**azure** " 菜单选项来验证 azure 工具包的安装。</span><span class="sxs-lookup"><span data-stu-id="b6ce2-129">Validate the Azure Toolkit installation by verifying that you can find a **Tools** > **Azure** menu option in Eclipse.</span></span>
