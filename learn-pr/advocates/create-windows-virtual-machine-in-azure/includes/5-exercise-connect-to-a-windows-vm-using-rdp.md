<span data-ttu-id="fcb14-101">我们已部署并运行 Windows VM, 但未将其配置为执行任何工作。</span><span class="sxs-lookup"><span data-stu-id="fcb14-101">We have our Windows VM deployed and running, but it's not configured to do any work.</span></span>

<span data-ttu-id="fcb14-102">回想一下我们的方案是视频处理系统。</span><span class="sxs-lookup"><span data-stu-id="fcb14-102">Recall our scenario is a video processing system.</span></span> <span data-ttu-id="fcb14-103">我们的平台通过 FTP 接收文件。</span><span class="sxs-lookup"><span data-stu-id="fcb14-103">Our platform receives files through FTP.</span></span> <span data-ttu-id="fcb14-104">通讯摄像机将视频剪辑上载到一个已知的 URL, 该 URL 映射到服务器上的文件夹。</span><span class="sxs-lookup"><span data-stu-id="fcb14-104">The traffic cameras upload video clips to a known URL, which is mapped to a folder on the server.</span></span> <span data-ttu-id="fcb14-105">每个 Windows VM 上的自定义软件作为一项服务运行, 并监视该文件夹并处理每个已上载的剪辑。</span><span class="sxs-lookup"><span data-stu-id="fcb14-105">The custom software on each Windows VM runs as a service and watches the folder and processes each uploaded clip.</span></span> <span data-ttu-id="fcb14-106">然后, 它将规范化的视频传递给在其他 Azure 服务上运行的算法。</span><span class="sxs-lookup"><span data-stu-id="fcb14-106">It then passes the normalized video to our algorithms running on other Azure services.</span></span>

<span data-ttu-id="fcb14-107">若要支持此方案, 我们需要进行以下配置:</span><span class="sxs-lookup"><span data-stu-id="fcb14-107">There are a few things we would need to configure to support this scenario:</span></span>

- <span data-ttu-id="fcb14-108">安装 FTP 并打开通信所需的端口。</span><span class="sxs-lookup"><span data-stu-id="fcb14-108">Install FTP and open the ports it needs to communicate.</span></span>
- <span data-ttu-id="fcb14-109">安装城市的摄像头系统特有的专用视频编解码器。</span><span class="sxs-lookup"><span data-stu-id="fcb14-109">Install the proprietary video codec unique to the city's camera system.</span></span>
- <span data-ttu-id="fcb14-110">安装处理已上载视频的转码服务。</span><span class="sxs-lookup"><span data-stu-id="fcb14-110">Install our transcoding service that processes uploaded videos.</span></span>

<span data-ttu-id="fcb14-111">其中很多是典型的管理任务, 我们不会在这里实际介绍, 并且我们没有要安装的软件。</span><span class="sxs-lookup"><span data-stu-id="fcb14-111">Many of these are typical administrative tasks we won't actually cover here, and we don't have software to install.</span></span> <span data-ttu-id="fcb14-112">相反, 我们将逐步完成这些步骤, 并向你展示__ 如何使用远程桌面安装自定义或第三方软件。</span><span class="sxs-lookup"><span data-stu-id="fcb14-112">Instead, we will walk through the steps and show you how you _could_ install custom or third-party software using Remote Desktop.</span></span> <span data-ttu-id="fcb14-113">首先, 我们来获取连接信息。</span><span class="sxs-lookup"><span data-stu-id="fcb14-113">Let's start by getting the connection information.</span></span>

## <a name="connect-to-the-vm-with-remote-desktop-protocol"></a><span data-ttu-id="fcb14-114">使用远程桌面协议连接到 VM</span><span class="sxs-lookup"><span data-stu-id="fcb14-114">Connect to the VM with Remote Desktop Protocol</span></span>

<span data-ttu-id="fcb14-115">若要使用 RDP 客户端连接到 Azure 虚拟机, 你将需要:</span><span class="sxs-lookup"><span data-stu-id="fcb14-115">To connect to an Azure VM with an RDP client, you will need:</span></span>

- <span data-ttu-id="fcb14-116">vm 的公共 IP 地址 (如果虚拟机配置为连接到网络, 则为 "私人")。</span><span class="sxs-lookup"><span data-stu-id="fcb14-116">The public IP address of the VM (or private if the VM is configured to connect to your network).</span></span>
- <span data-ttu-id="fcb14-117">端口号。</span><span class="sxs-lookup"><span data-stu-id="fcb14-117">The port number.</span></span>

<span data-ttu-id="fcb14-118">您可以将此信息输入到 RDP 客户端, 也可以下载预先配置的**RDP**文件。</span><span class="sxs-lookup"><span data-stu-id="fcb14-118">You can enter this information into the RDP client, or download a pre-configured **RDP** file.</span></span>

### <a name="download-the-rdp-file"></a><span data-ttu-id="fcb14-119">下载 RDP 文件</span><span class="sxs-lookup"><span data-stu-id="fcb14-119">Download the RDP file</span></span>

1. <span data-ttu-id="fcb14-120">在[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)中, 确保先前创建的虚拟机的**概述**面板处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="fcb14-120">In the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), ensure the **Overview** panel for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="fcb14-121">如果需要打开 VM, 则可以在 "**所有资源**" 下找到它。</span><span class="sxs-lookup"><span data-stu-id="fcb14-121">You can find the VM under **All Resources** if you need to open it.</span></span> <span data-ttu-id="fcb14-122">概述面板包含有关 VM 的大量信息。</span><span class="sxs-lookup"><span data-stu-id="fcb14-122">The overview panel has a lot of information about the VM.</span></span>

    - <span data-ttu-id="fcb14-123">您可以查看虚拟机是否正在运行。</span><span class="sxs-lookup"><span data-stu-id="fcb14-123">You can see whether the VM is running.</span></span>
    - <span data-ttu-id="fcb14-124">停止或重新启动它。</span><span class="sxs-lookup"><span data-stu-id="fcb14-124">Stop or restart it.</span></span>
    - <span data-ttu-id="fcb14-125">获取用于连接到 VM 的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="fcb14-125">Get the public IP address to connect to the VM.</span></span>
    - <span data-ttu-id="fcb14-126">查看 CPU、磁盘和网络的活动。</span><span class="sxs-lookup"><span data-stu-id="fcb14-126">See the activity of the CPU, disk, and network.</span></span>

1. <span data-ttu-id="fcb14-127">单击窗格顶部的 "**连接**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="fcb14-127">Click the **Connect** button at the top of the pane.</span></span>

1. <span data-ttu-id="fcb14-128">在 "**连接到虚拟机**叶片" 中, 记下 " **IP 地址**" 和 "**端口号**" 设置, 然后单击 "**下载 RDP 文件**" 并将其保存到计算机。</span><span class="sxs-lookup"><span data-stu-id="fcb14-128">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings, then click **Download RDP File** and save it to your computer.</span></span>

1. <span data-ttu-id="fcb14-129">在连接之前, 我们先调整几个设置。</span><span class="sxs-lookup"><span data-stu-id="fcb14-129">Before we connect, let's adjust a few settings.</span></span> <span data-ttu-id="fcb14-130">在 Windows 上, 使用资源管理器查找文件, 然后右键单击并选择 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="fcb14-130">On Windows, find the file using Explorer, right-click and select **Edit**.</span></span> <span data-ttu-id="fcb14-131">在 MacOS 上, 需要先使用 RDP 客户端打开文件, 然后在显示的列表中右键单击该项目, 然后选择 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="fcb14-131">On MacOS you will need to open the file first with the RDP client and then right-click on the item in the displayed list and select **Edit**.</span></span>

1. <span data-ttu-id="fcb14-132">您可以调整各种设置, 以控制连接到 Azure VM 的体验。</span><span class="sxs-lookup"><span data-stu-id="fcb14-132">You can adjust a variety of settings to control the experience in connecting to the Azure VM.</span></span> <span data-ttu-id="fcb14-133">您要检查的设置包括:</span><span class="sxs-lookup"><span data-stu-id="fcb14-133">The settings you will want to examine are:</span></span>

    - <span data-ttu-id="fcb14-134">**显示**: 默认情况下, 它将全屏显示。</span><span class="sxs-lookup"><span data-stu-id="fcb14-134">**Display**: By default, it will be full screen.</span></span> <span data-ttu-id="fcb14-135">您可以将其更改为较低的分辨率, 如果您有多个监视器, 则使用所有监视器。</span><span class="sxs-lookup"><span data-stu-id="fcb14-135">You can change this to a lower resolution, or use all your monitors if you have more than one.</span></span>
    - <span data-ttu-id="fcb14-136">**本地资源**: 可以与 vm 共享本地驱动器-允许你将文件从电脑复制到 vm。</span><span class="sxs-lookup"><span data-stu-id="fcb14-136">**Local Resources**: You can share local drives with the VM - allowing you to copy files from your PC to the VM.</span></span> <span data-ttu-id="fcb14-137">单击 "**本地设备和资源**" 下的 "**更多**" 按钮以选择共享内容。</span><span class="sxs-lookup"><span data-stu-id="fcb14-137">Click the **More** button under **Local devices and resources** to select what is shared.</span></span>
    - <span data-ttu-id="fcb14-138">**体验**: 根据你的网络质量调整视觉体验。</span><span class="sxs-lookup"><span data-stu-id="fcb14-138">**Experience**: Adjust the visual experience based on your network quality.</span></span>

1. <span data-ttu-id="fcb14-139">共享本地 C: 驱动器, 使其对 VM 可见。</span><span class="sxs-lookup"><span data-stu-id="fcb14-139">Share your Local C: drive so it will be visible to the VM.</span></span>

1. <span data-ttu-id="fcb14-140">切换回 "**常规**" 选项卡, 然后单击 "**保存**" 以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="fcb14-140">Switch back to the **General** tab and click **Save** to save the changes.</span></span> <span data-ttu-id="fcb14-141">你可以随时返回并稍后编辑此文件, 以尝试其他设置。</span><span class="sxs-lookup"><span data-stu-id="fcb14-141">You can always come back and edit this file later to try other settings.</span></span>

### <a name="connect-to-the-windows-vm"></a><span data-ttu-id="fcb14-142">连接到 Windows VM</span><span class="sxs-lookup"><span data-stu-id="fcb14-142">Connect to the Windows VM</span></span>

1. <span data-ttu-id="fcb14-143">单击 "**连接**" 按钮以启动到 VM 的连接。</span><span class="sxs-lookup"><span data-stu-id="fcb14-143">Click the **Connect** button to start the connection to the VM.</span></span>

1. <span data-ttu-id="fcb14-144">在 "**远程桌面连接**" 对话框中, 记下 "安全警告" 和 "远程计算机 IP 地址", 然后单击 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="fcb14-144">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="fcb14-145">在 " **Windows 安全性**" 对话框中, 输入您在步骤6和7中使用的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="fcb14-145">In the **Windows Security** dialog box, enter your username and password that you used in steps 6 and 7.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fcb14-146">如果您使用 Windows 客户端连接到 VM, 它将默认为您的计算机上的已知标识。</span><span class="sxs-lookup"><span data-stu-id="fcb14-146">If you are using a Windows client to connect to the VM, it will default to known identities on your machine.</span></span> <span data-ttu-id="fcb14-147">您可以单击 "**更多选择**" 选项, 然后选择 "使用其他帐户", 让您输入不同的用户名/密码组合。</span><span class="sxs-lookup"><span data-stu-id="fcb14-147">You can click the **More choices** option and select "Use a different account" to let you enter a different username/password combination.</span></span>

1. <span data-ttu-id="fcb14-148">在第二个 "**远程桌面连接**" 对话框中, 记下证书错误, 然后单击 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="fcb14-148">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span>

### <a name="install-worker-roles"></a><span data-ttu-id="fcb14-149">安装辅助角色</span><span class="sxs-lookup"><span data-stu-id="fcb14-149">Install worker roles</span></span>

<span data-ttu-id="fcb14-150">首次连接到 Windows server VM 时, 将启动服务器管理器。</span><span class="sxs-lookup"><span data-stu-id="fcb14-150">The first time you connect to a Windows server VM, it will launch Server Manager.</span></span> <span data-ttu-id="fcb14-151">这使您可以为常见的 web 或数据任务分配 worker 角色。</span><span class="sxs-lookup"><span data-stu-id="fcb14-151">This allows you to assign a worker role for common web or data tasks.</span></span> <span data-ttu-id="fcb14-152">还可以通过 "开始" 菜单启动服务器管理器。</span><span class="sxs-lookup"><span data-stu-id="fcb14-152">You can also launch the Server Manager through the Start Menu.</span></span>

<span data-ttu-id="fcb14-153">这是我们将 Web 服务器角色添加到服务器的地方。</span><span class="sxs-lookup"><span data-stu-id="fcb14-153">This is where we would add the Web Server role to the server.</span></span> <span data-ttu-id="fcb14-154">这将在配置过程中安装 IIS 和, 以关闭 HTTP 请求并启用 FTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="fcb14-154">This will install IIS and as part of the configuration you would turn off HTTP requests and enable the FTP server.</span></span> <span data-ttu-id="fcb14-155">或者, 我们可以忽略 IIS 并安装第三方 FTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="fcb14-155">Or, we could ignore IIS and install a third-party FTP server.</span></span> <span data-ttu-id="fcb14-156">然后, 将 FTP 服务器配置为允许访问我们添加到 VM 的大型数据驱动器上的文件夹。</span><span class="sxs-lookup"><span data-stu-id="fcb14-156">We'd then configure the FTP server to allow access to a folder on our big data drive we added to the VM.</span></span>

<span data-ttu-id="fcb14-157">由于我们不会在此处实际配置这些内容, 因此只需关闭服务器管理器即可。</span><span class="sxs-lookup"><span data-stu-id="fcb14-157">Since we aren't going to actually configure that here, just close Server Manager.</span></span>

## <a name="install-custom-software"></a><span data-ttu-id="fcb14-158">安装自定义软件</span><span class="sxs-lookup"><span data-stu-id="fcb14-158">Install custom software</span></span>

<span data-ttu-id="fcb14-159">我们有两种方法可用于安装软件。</span><span class="sxs-lookup"><span data-stu-id="fcb14-159">We have two approaches we can use to install software.</span></span> <span data-ttu-id="fcb14-160">首先, 此 VM 已连接到 Internet。</span><span class="sxs-lookup"><span data-stu-id="fcb14-160">First, this VM is connected to the Internet.</span></span> <span data-ttu-id="fcb14-161">如果所需的软件具有可下载的安装程序, 则可以在 RDP 会话中打开 web 浏览器、下载软件并安装它。</span><span class="sxs-lookup"><span data-stu-id="fcb14-161">If the software you need has a downloadable installer, you can open a web browser in the RDP session, download the software, and install it.</span></span> <span data-ttu-id="fcb14-162">其次, 如果软件是自定义的 (如自定义服务), 您可以将其从本地计算机复制到 VM 以安装它。</span><span class="sxs-lookup"><span data-stu-id="fcb14-162">Second, if your software is custom - like our custom service, you can copy it from your local machine over to the VM to install it.</span></span> <span data-ttu-id="fcb14-163">让我们来看看这后一方法。</span><span class="sxs-lookup"><span data-stu-id="fcb14-163">Let's look at this latter approach.</span></span>

1. <span data-ttu-id="fcb14-164">打开文件资源管理器。</span><span class="sxs-lookup"><span data-stu-id="fcb14-164">Open File Explorer.</span></span> <span data-ttu-id="fcb14-165">单击边栏中的 "**这台电脑**"。</span><span class="sxs-lookup"><span data-stu-id="fcb14-165">Click on **This PC** in the sidebar.</span></span> <span data-ttu-id="fcb14-166">您应该会看到几个驱动器:</span><span class="sxs-lookup"><span data-stu-id="fcb14-166">You should see several drives:</span></span>

    - <span data-ttu-id="fcb14-167">Windows (C:)表示操作系统的驱动器。</span><span class="sxs-lookup"><span data-stu-id="fcb14-167">Windows (C:) drive representing the OS.</span></span>
    - <span data-ttu-id="fcb14-168">临时存储 (D:)驱动器.</span><span class="sxs-lookup"><span data-stu-id="fcb14-168">Temporary Storage (D:) drive.</span></span>
    - <span data-ttu-id="fcb14-169">本地 C: drive (它的名称将与下图所示的名称不同)。</span><span class="sxs-lookup"><span data-stu-id="fcb14-169">Your local C: drive (it will have a different name than shown below).</span></span>

    ![显示与 Azure VM 共享的本地驱动器的屏幕截图。](../media/6-drive-list.png)

<span data-ttu-id="fcb14-171">通过对本地驱动器的访问权限, 您可以将自定义软件的文件复制到 VM 并安装软件。</span><span class="sxs-lookup"><span data-stu-id="fcb14-171">With access to your local drive, you can copy the files for the custom software onto the VM and install the software.</span></span> <span data-ttu-id="fcb14-172">我们实际上不会这样做, 因为它只是一个模拟方案, 但您可以想像它的工作方式。</span><span class="sxs-lookup"><span data-stu-id="fcb14-172">We won't actually do that since it's just a simulated scenario, but you can imagine how it would work.</span></span>

<span data-ttu-id="fcb14-173">在驱动器列表中观察的更有趣的事情是_缺少_的内容。</span><span class="sxs-lookup"><span data-stu-id="fcb14-173">The more interesting thing to observe in the list of drives is what is _missing_.</span></span> <span data-ttu-id="fcb14-174">请注意, 我们的**数据**驱动器不存在。</span><span class="sxs-lookup"><span data-stu-id="fcb14-174">Notice that our **Data** drive is not present.</span></span> <span data-ttu-id="fcb14-175">Azure 添加了一个 VHD, 但未将其初始化。</span><span class="sxs-lookup"><span data-stu-id="fcb14-175">Azure added a VHD but didn't initialize it.</span></span>

## <a name="initialize-data-disks"></a><span data-ttu-id="fcb14-176">初始化数据磁盘</span><span class="sxs-lookup"><span data-stu-id="fcb14-176">Initialize data disks</span></span>

<span data-ttu-id="fcb14-177">从头开始创建的任何其他驱动器都需要进行初始化和格式化。</span><span class="sxs-lookup"><span data-stu-id="fcb14-177">Any additional drives you create from scratch will need to be initialized and formatted.</span></span> <span data-ttu-id="fcb14-178">执行此操作的过程与物理驱动器相同。</span><span class="sxs-lookup"><span data-stu-id="fcb14-178">The process for doing this is identical to a physical drive.</span></span>

1. <span data-ttu-id="fcb14-179">从 "开始" 菜单启动 "**磁盘管理**" 工具。</span><span class="sxs-lookup"><span data-stu-id="fcb14-179">Launch the **Disk Management** tool from the Start Menu.</span></span> <span data-ttu-id="fcb14-180">您可能需要先转到 "计算机管理" 工具, 再转到 "磁盘管理", 或尝试在 "开始" 菜单中搜索 "磁盘管理"。</span><span class="sxs-lookup"><span data-stu-id="fcb14-180">You may have to go to the Computer Management tool first, then Disk Management, or try searching for "Disk Management" in the Start Menu.</span></span>

1. <span data-ttu-id="fcb14-181">它将显示一条警告, 指出它已检测到未初始化的磁盘。</span><span class="sxs-lookup"><span data-stu-id="fcb14-181">It will display a warning that it has detected an uninitialized disk.</span></span>

    ![显示有关 VM 中未初始化的数据磁盘的磁盘管理工具警告的屏幕截图。](../media/6-disk-management.png)

1. <span data-ttu-id="fcb14-183">单击 **"确定"** 以初始化磁盘。</span><span class="sxs-lookup"><span data-stu-id="fcb14-183">Click **OK** to initialize the disk.</span></span> <span data-ttu-id="fcb14-184">它将显示在可以设置格式的卷列表中, 并为其分配驱动器号。</span><span class="sxs-lookup"><span data-stu-id="fcb14-184">It will then show up in the list of volumes where you can format it and assign a drive letter.</span></span>

1. <span data-ttu-id="fcb14-185">打开文件资源管理器, 您现在应该会看到您的数据驱动器。</span><span class="sxs-lookup"><span data-stu-id="fcb14-185">Open File Explorer and you should now see your data drive.</span></span>

1. <span data-ttu-id="fcb14-186">继续并关闭 RDP 客户端以注销 VM。</span><span class="sxs-lookup"><span data-stu-id="fcb14-186">Go ahead and close the RDP client to sign out of the VM.</span></span> <span data-ttu-id="fcb14-187">服务器将继续运行。</span><span class="sxs-lookup"><span data-stu-id="fcb14-187">The server will continue to run.</span></span>

<span data-ttu-id="fcb14-188">RDP 允许你像本地计算机一样使用 Azure 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="fcb14-188">RDP allows you to work with the Azure VM just like a local computer.</span></span> <span data-ttu-id="fcb14-189">使用桌面 UI 访问时, 您可以像管理任何 Windows 计算机一样管理此 VM: 安装软件、配置角色、调整功能和其他常见任务。</span><span class="sxs-lookup"><span data-stu-id="fcb14-189">With Desktop UI access, you can administer this VM as you would any Windows computer: installing software, configuring roles, adjusting features and other common tasks.</span></span> <span data-ttu-id="fcb14-190">但是, 这是一个手动过程-如果我们始终需要安装一些软件, 则可以考虑使用脚本自动执行该过程。</span><span class="sxs-lookup"><span data-stu-id="fcb14-190">However, it's a manual process - if we always need to install some software, you might consider automating the process using scripting.</span></span>