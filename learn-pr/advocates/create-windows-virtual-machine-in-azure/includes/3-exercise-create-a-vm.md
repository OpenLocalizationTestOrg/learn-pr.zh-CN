<span data-ttu-id="2a0e9-101">请记住, 我们的公司在 Windows vm 上处理视频内容。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-101">Recall that our company processes video content on Windows VMs.</span></span> <span data-ttu-id="2a0e9-102">新城市已将我们的交通相机告知我们, 但这是我们之前未处理的模型。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-102">A new city has contracted us to process their traffic cameras, but it's a model we've not worked with before.</span></span> <span data-ttu-id="2a0e9-103">我们需要创建一个新的 Windows VM 并安装一些专用的编解码器, 以便我们可以开始处理和分析其图像。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-103">We need to create a new Windows VM and install some proprietary codecs so we can begin processing and analyzing their images.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-new-windows-virtual-machine"></a><span data-ttu-id="2a0e9-104">创建新的 Windows 虚拟机</span><span class="sxs-lookup"><span data-stu-id="2a0e9-104">Create a new Windows virtual machine</span></span>

<span data-ttu-id="2a0e9-105">我们可以使用 azure 门户、azure CLI 或 azure PowerShell 创建 Windows 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-105">We can create Windows VMs with the Azure portal, Azure CLI, or Azure PowerShell.</span></span> <span data-ttu-id="2a0e9-106">最简单的方法是门户, 因为它将引导您完成所需的信息, 并在创建 VM 的过程中提供提示和有用的消息。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-106">The easiest approach is the portal because it walks you through the required information and provides hints and helpful messages during the creation of the VM.</span></span>

1. <span data-ttu-id="2a0e9-107">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-107">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="2a0e9-108">单击 Azure 门户左上角的 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-108">Click **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="2a0e9-109">在 "搜索" 框中, 输入**Windows Server 2016 Datacenter** , 然后在显示的列表中单击具有相同标题的链接。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-109">In the search box, enter  **Windows Server 2016 Datacenter**  and then click on the link with the same title in the presented list.</span></span>

1. <span data-ttu-id="2a0e9-110">单击 "**创建**" 按钮开始配置 VM。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-110">Click the **Create** button to start configuring the VM.</span></span>

## <a name="configure-the-vm-settings"></a><span data-ttu-id="2a0e9-111">配置虚拟机设置</span><span class="sxs-lookup"><span data-stu-id="2a0e9-111">Configure the VM settings</span></span>

<span data-ttu-id="2a0e9-112">门户中的 VM 创建体验以 "向导" 的格式显示, 以引导您完成 VM 的所有配置区域。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-112">The VM creation experience in the portal is presented in a "wizard" format to walk you through all the configuration areas for the VM.</span></span> <span data-ttu-id="2a0e9-113">单击 "下一步" 按钮将转到下一个可配置的部分。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-113">Clicking the "Next" button will take you to the next configurable section.</span></span> <span data-ttu-id="2a0e9-114">但是, 您可以在中的各节之间移动, 这些选项卡在标识每个部分的顶部运行。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-114">However, you can move between the sections at will with the tabs running across the top that identify each section.</span></span>

![显示在 Azure 门户中创建虚拟机体验的屏幕截图。](../media/3-azure-portal-create-vm.png)

<span data-ttu-id="2a0e9-116">一旦您填写了所有必需的选项 (用红色星标识), 您可以跳过其余的向导体验, 并通过底部的 "**审阅 + 创建**" 按钮来开始创建 VM。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-116">Once you fill in all the required options (identified with red stars), you can skip the remainder of the wizard experience and start creating the VM through the **Review + Create** button at the bottom.</span></span>

<span data-ttu-id="2a0e9-117">我们将从 "**基础知识**" 部分开始。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-117">We'll start with the **Basics** section.</span></span>

### <a name="configure-basic-vm-settings"></a><span data-ttu-id="2a0e9-118">配置基本虚拟机设置</span><span class="sxs-lookup"><span data-stu-id="2a0e9-118">Configure basic VM settings</span></span>

> [!NOTE]
> <span data-ttu-id="2a0e9-119">当您在每个自由文本字段中更改设置和选项卡时, Azure 将自动验证每个值, 并在其正常时在其旁边放置绿色复选标记。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-119">As you change settings and tab out of each free-text field, Azure will validate each value automatically and place a green check mark next to it when it's good.</span></span> <span data-ttu-id="2a0e9-120">您可以将鼠标悬停在错误指示器上方, 以获取有关它发现的问题的详细信息。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-120">You can hover over error indicators to get more information on issues it discovers.</span></span>

1. <span data-ttu-id="2a0e9-121">选择应为 VM 时间计费的**订阅**。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-121">Select the **Subscription** that should be billed for VM hours.</span></span>

1. <span data-ttu-id="2a0e9-122">对于 "**资源组**", 选择 "**<rgn>[沙盒资源组名称]</rgn>**"。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-122">For **Resource group**, choose "**<rgn>[sandbox resource group name]</rgn>**".</span></span>

1. <span data-ttu-id="2a0e9-123">在 "**实例详细信息**" 部分, 输入你的 VM 的名称, 如**测试副总裁-vm2** (针对测试视频处理器 VM #2)。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-123">In the **INSTANCE DETAILS** section, enter a name for your VM, such as **test-vp-vm2** (for Test Video Processor VM #2).</span></span>
    - <span data-ttu-id="2a0e9-124">最好的做法是对资源名称进行标准化, 以便能够轻松地识别它们的用途。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-124">It's best practice to standardize your resource names so you can easily identify their purpose.</span></span> <span data-ttu-id="2a0e9-125">Windows VM 名称是一种受限制的名称-它们必须介于1到15个字符之间, 不能包含非 ASCII 字符或特殊字符, 并且在当前资源组中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-125">Windows VM names are a bit limited - they must be between 1 and 15 characters, cannot contain non-ASCII or special characters, and must be unique in the current resource group.</span></span>

1. <span data-ttu-id="2a0e9-126">从以下位置选择与你接近的区域。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-126">Select a region close to you from the locations below.</span></span>

   [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="2a0e9-127">将**可用性选项**保留为 "无"。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-127">Leave **Availability options** as "None".</span></span> <span data-ttu-id="2a0e9-128">此选项可用于通过将多个虚拟机组合在一起以处理计划的或计划外的维护事件或中断, 以确保虚拟机高度可用。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-128">This option is used to ensure the VM is highly available by grouping multiple VMs together a set to deal with planned or unplanned maintenance events or outages.</span></span>

1. <span data-ttu-id="2a0e9-129">确保将图像设置为 "Windows Server 2016 Datacenter"。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-129">Ensure the image is set to "Windows Server 2016 Datacenter".</span></span> <span data-ttu-id="2a0e9-130">您可以打开下拉列表以查看所有可用选项。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-130">You can open the drop-down list to see all the options available.</span></span>

1. <span data-ttu-id="2a0e9-131">**Size**字段不是直接可编辑的, 并且具有 DS1 的默认大小。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-131">The **Size** field is not directly editable and has a DS1 default size.</span></span> <span data-ttu-id="2a0e9-132">单击 "**更改大小**" 链接以浏览其他 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-132">Click the **Change size** link to explore other VM sizes.</span></span> <span data-ttu-id="2a0e9-133">生成的对话框允许您根据 cpu、名称和磁盘类型的数量进行筛选。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-133">The resulting dialog allows you to filter based on # of CPUs, Name, and Disk Type.</span></span> <span data-ttu-id="2a0e9-134">完成后, 选择 "Standard DS1 v2" (通常为默认值)。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-134">Select "Standard DS1 v2" (normally the default) when you are done.</span></span> <span data-ttu-id="2a0e9-135">这将提供虚拟机 1 CPU 和 3.5 GB 的内存。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-135">That will give the VM 1 CPU and 3.5 GB of memory.</span></span>

    > [!TIP]
    > <span data-ttu-id="2a0e9-136">您还可以将视图向左滑动以返回到虚拟机设置, 因为它在右侧打开一个新窗口并 slid 该窗口以进行查看。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-136">You can also just slide the view to the left to get back to the VM settings as it opened a new window off to the right and slid the window over to view it.</span></span>

1. <span data-ttu-id="2a0e9-137">在 "**管理员帐户**" 部分, 将 "**用户名**" 字段设置为您将用于登录到 VM 的用户名。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-137">In the **ADMINISTRATOR ACCOUNT** section, set the **Username** field to a username you will use to sign in to the VM.</span></span>

1. <span data-ttu-id="2a0e9-138">在 "**密码**" 字段中, 输入长度至少为12个字符的密码。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-138">In the **Password** field, enter a password that's at least 12 characters long.</span></span> <span data-ttu-id="2a0e9-139">它必须具有以下三项: 一个小写字符、一个大写字符、一个数字和一个非 '\\' 或 '-' 的特殊字符。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-139">It must have three of the following: one lower case character, one uppercase character, one number, and one special character that is not '\\' or '-'.</span></span> <span data-ttu-id="2a0e9-140">使用你要记住或记下它的一些内容, 稍后将需要它。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-140">Use something you will remember or write it down, you will need it later.</span></span>

1. <span data-ttu-id="2a0e9-141">确认**密码**。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-141">Confirm the **password**.</span></span>

1. <span data-ttu-id="2a0e9-142">在 "**入站端口规则**" 部分, 打开列表并选择 "_允许选择的端口_"。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-142">In the **INBOUND PORT RULES** section, open the list and choose _Allow selected ports_.</span></span> <span data-ttu-id="2a0e9-143">由于这是 Windows VM, 因此我们希望能够使用 RDP 访问桌面。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-143">Since this is a Windows VM, we want to be able to access the desktop using RDP.</span></span> <span data-ttu-id="2a0e9-144">根据需要滚动列表, 直到找到 RDP (3389) 并将其选中。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-144">Scroll the list if necessary until you find RDP (3389) and select it.</span></span> <span data-ttu-id="2a0e9-145">如 UI 中的注释所示, 我们还可以在创建虚拟机之后调整网络端口。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-145">As the note in the UI indicates, we can also adjust the network ports after we create the VM.</span></span>

    ![显示用于在 Windows VM 上打开 RDP 访问端口的下拉的屏幕截图。](../media/3-open-ports.png)

## <a name="configure-disks-for-the-vm"></a><span data-ttu-id="2a0e9-147">为 VM 配置磁盘</span><span class="sxs-lookup"><span data-stu-id="2a0e9-147">Configure Disks for the VM</span></span>

1. <span data-ttu-id="2a0e9-148">单击 "**下一步**" 移动到 "磁盘" 部分。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-148">Click **Next** to move to the Disks section.</span></span>

    ![显示 VM 的 "配置磁盘" 部分的屏幕截图。](../media/3-configure-disks.png)

1. <span data-ttu-id="2a0e9-150">为**OS 磁盘类型**选择 "Premium SSD"。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-150">Choose "Premium SSD" for the **OS disk type**.</span></span>

1. <span data-ttu-id="2a0e9-151">使用托管磁盘, 因此我们不必使用存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-151">Use managed disks so we don't have to work with storage accounts.</span></span> <span data-ttu-id="2a0e9-152">您可以翻转 GUI 中的开关, 以查看 Azure 需要的信息在您喜欢的不同之处。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-152">You can flip the switch in the GUI to see the difference in information that Azure needs if you like.</span></span>

### <a name="create-a-data-disk"></a><span data-ttu-id="2a0e9-153">创建数据磁盘</span><span class="sxs-lookup"><span data-stu-id="2a0e9-153">Create a data disk</span></span>

<span data-ttu-id="2a0e9-154">回想一下, 我们将获取 OS 磁盘 (C:)和临时磁盘 (D:)。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-154">Recall we will get an OS disk (C:) and Temporary disk (D:).</span></span> <span data-ttu-id="2a0e9-155">还可以添加数据磁盘。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-155">Let's add a data disk as well.</span></span>

1. <span data-ttu-id="2a0e9-156">单击 "**数据磁盘**" 部分中的 "**创建并附加新磁盘**" 链接。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-156">Click the **Create and attach a new disk** link in the **DATA DISKS** section.</span></span>

    ![显示门户中新的 "VM 磁盘创建" 对话框的屏幕截图。](../media/3-add-data-disk.png)

1. <span data-ttu-id="2a0e9-158">您可以采用所有默认值: 高级 SSD、1023 GB 和无 (空磁盘);但请注意, 在这里, 我们可以使用快照或存储 Blob 来创建 VHD。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-158">You can take all the defaults: Premium SSD, 1023 GB, and None (empty disk); although notice that here is where we could use a snapshot, or Storage Blob to create a VHD.</span></span>

1. <span data-ttu-id="2a0e9-159">单击 **"确定"** 以创建磁盘并返回到 "**数据磁盘**" 部分。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-159">Click **OK** to create the disk and go back to the **DATA DISKS** section.</span></span>

1. <span data-ttu-id="2a0e9-160">现在, 第一行中应该有一个新磁盘。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-160">There should now be a new disk in the first row.</span></span>

    ![显示 VM 中新添加的磁盘的屏幕截图。](../media/3-new-disk.png)

## <a name="configure-the-network"></a><span data-ttu-id="2a0e9-162">配置网络</span><span class="sxs-lookup"><span data-stu-id="2a0e9-162">Configure the Network</span></span>

1. <span data-ttu-id="2a0e9-163">单击 "**下一步**" 移动到 "网络" 部分。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-163">Click **Next** to move to the Networking section.</span></span>

1. <span data-ttu-id="2a0e9-164">在我们已有其他组件的生产系统中, 我们想要利用_现有_的虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-164">In a production system where we already have other components, we'd want to utilize an _existing_ virtual network.</span></span> <span data-ttu-id="2a0e9-165">这样, VM 便可以与我们的解决方案中的其他云服务进行通信。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-165">That way our VM can communicate with the other cloud services in our solution.</span></span> <span data-ttu-id="2a0e9-166">如果尚未在此位置中定义任何一个, 则可以在此处创建并配置以下内容:</span><span class="sxs-lookup"><span data-stu-id="2a0e9-166">If there isn't one defined in this location yet, we can create it here and configure the:</span></span>
    - <span data-ttu-id="2a0e9-167">**地址空间**: 此网络可用的总 IPV4 空间。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-167">**Address space**: the overall IPV4 space available to this network.</span></span>
    - <span data-ttu-id="2a0e9-168">**子网范围**: 要细分地址空间的第一个子网-它必须在定义的地址空间内。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-168">**Subnet range**: the first subnet to subdivide the address space - it must fit within the defined address space.</span></span> <span data-ttu-id="2a0e9-169">创建 VNet 后, 可以添加其他子网。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-169">Once the VNet is created you can add additional subnets.</span></span>

1. <span data-ttu-id="2a0e9-170">让我们将默认范围更改为使用`172.xxx` IP 地址空间。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-170">Let's change the default ranges to use the `172.xxx` IP address space.</span></span> <span data-ttu-id="2a0e9-171">单击 "虚拟网络" 下的 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-171">Click **Create New** under Virtual Network.</span></span>
    - <span data-ttu-id="2a0e9-172">将 "**地址空间**" 字段更改`172.16.0.0/16`为, 以为其提供所有地址范围</span><span class="sxs-lookup"><span data-stu-id="2a0e9-172">Change the **Address space** field to be `172.16.0.0/16` to give it the full range of addresses</span></span>
    - <span data-ttu-id="2a0e9-173">将 "**子网范围**" 字段`172.16.1.0/24`更改为为其分配的 256 IP 地址的空间。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-173">Change the **Subnet range** field to be `172.16.1.0/24` to give it 256 IP addresses of the space.</span></span>

1. <span data-ttu-id="2a0e9-174">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-174">Click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="2a0e9-175">默认情况下, Azure 将为你的 VM 创建虚拟网络、网络接口和公用 IP。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-175">By default, Azure will create a virtual network, network interface, and public IP for your VM.</span></span> <span data-ttu-id="2a0e9-176">在创建虚拟机之后更改网络选项并不是很简单, 因此总是请仔细检查您在 Azure 中创建的服务上的网络分配。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-176">It's not trivial to change the networking options after the VM has been created so always double-check the network assignments on services you create in Azure.</span></span>

## <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="2a0e9-177">完成虚拟机的配置并创建映像</span><span class="sxs-lookup"><span data-stu-id="2a0e9-177">Finish configuring the VM and create the image</span></span>

<span data-ttu-id="2a0e9-178">其余选项具有合理的默认设置, 无需更改任何其他选项。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-178">The rest of the options have reasonable defaults and there's no need to change any of them.</span></span> <span data-ttu-id="2a0e9-179">如果愿意, 你可以浏览其他选项卡。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-179">You can explore the other tabs if you like.</span></span> <span data-ttu-id="2a0e9-180">各个选项旁边都有`(i)`一个图标, 将显示一个帮助气泡来说明该选项。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-180">The individual options have an `(i)` icon next to them that will show a help bubble to explain the option.</span></span> <span data-ttu-id="2a0e9-181">这是了解可用于配置 VM 的各种选项的好方法。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-181">This is a great way to learn about the various options you can use to configure the VM.</span></span>

1. <span data-ttu-id="2a0e9-182">单击面板底部的 "**审阅 + 创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-182">Click the **Review + create** button at the bottom of the panel.</span></span>

1. <span data-ttu-id="2a0e9-183">系统将验证您的选项, 并提供有关正在创建的 VM 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-183">The system will validate your options and give you details about the VM being created.</span></span>

1. <span data-ttu-id="2a0e9-184">单击 "**创建**" 以创建和部署 VM。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-184">Click **Create** to create and deploy the VM.</span></span> <span data-ttu-id="2a0e9-185">Azure 仪表板将显示正在部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-185">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="2a0e9-186">这可能需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-186">This may take several minutes.</span></span>

<span data-ttu-id="2a0e9-187">在部署时, 让我们来看看我们可以使用此 VM 做什么。</span><span class="sxs-lookup"><span data-stu-id="2a0e9-187">While that's deploying, let's look at what we can do with this VM.</span></span>